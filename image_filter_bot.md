**Project description:** Discord bot that detects images that detect nudity. The bot is slow to detect so it deletes all images regardless first. Then it reposts them if they don't contain nudity.

### 1. Code Snippets

Function used to check if a linked image is safe.

```javascript
    img_args.forEach(attachments => {

        try{

            (async() => { 
                img_path = await saveImg(attachments);

                message.delete()
                    .then(message => console.log(`Deleted message ${message.author.username}`))
                    .catch(console.error);

                scan_return = await scanImage(img_path);
                console.log("the image safe:" + scan_return);
                //^^^^above code should work
                scan_return = scan_return.replace(img_path, "");
                //console.log(scan_return);   //example output should be {'': {'unsafe': 0.99, 'safe': 0.01}}
                scan_return = scan_return.substring(6, scan_return.length - 2)
                //console.log(scan_return);  //example output should be 'unsafe': 0.99, 'safe': 0.01
                scan_return = scan_return.split(",");
                //console.log(scan_return);  //array with two values, index 1 being the highest.

                img_score = scan_return[1].toString();
                if(img_score.indexOf("unsafe") !== -1){
                    console.log("image is not safe");
                    //PM score of image
                    try{
                        const attachment = new discord.MessageAttachment('./images/joey_wheeler.jpeg', 'joey_wheeler.jpeg');
                        const my_embed_four = new discord.MessageEmbed()
                            .setDescription('Your image has been banished to the Shadow Realm!')
                            .attachFiles([attachment])
                            .setImage('attachment://joey_wheeler.jpeg');
                        await message.author.send(my_embed_four);
                    } catch(err){
                        console.log(err);
                    }

                } else {
                    console.log("image is safe");
                    //repost image
                    try{
                    var img_response = img_path.slice(14, img_path.length);
                    const attachment = new discord.MessageAttachment(`${img_path}`, `${img_response}`);
                    const my_embed_two = new discord.MessageEmbed()
                        .setDescription(`${message.author}'s image was found appropriate.`)
                        .setColor('#FF69B4')
                        //.setURL(img_response)
                        .attachFiles([attachment])
                        .setImage(`attachment://${img_response}`);
                    await message.channel.send(my_embed_two);

                    if(typeof img_path !== 'undefined'){
                        //removeDir(img_path);
                        //delete here
                        try{
                            deleteSavedImage(img_path);
                        } catch (err) {
                            console.log(err.stack);
                        }


                    }
                    } catch (e){
                        console.log(e.stack);
                    }



                //await message.channel.send(my_embed_two);

                }
            })();

        } catch(e) {
            console.log(e.stack);
        }
    });
```

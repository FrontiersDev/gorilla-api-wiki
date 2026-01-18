# Discord Bot Integration

You can use the API to power a Discord bot that fetches item stats and images on command.

## Prerequisites
* Node.js
* `discord.js` and `axios` installed

## Example Code
This snippet creates a simple slash command or text command handler.

```javascript
const axios = require('axios');
const API_URL = 'http://localhost:3000/api/cosmetics';

client.on('messageCreate', async message => {
    if (message.content.startsWith('!cosmetic')) {
        const query = message.content.split(' ').slice(1).join(' '); // Get search term
        
        try {
            // 1. Fetch all items
            const res = await axios.get(API_URL);
            
            // 2. Find the item
            const item = res.data.items.find(i => 
                i.name.toLowerCase().includes(query.toLowerCase())
            );

            if (!item) return message.reply("Cosmetic not found!");

            // 3. Reply with Embed
            const embed = {
                title: item.name,
                description: `Slot: ${item.slot}\nPrice: ${item.price} Shiny Rocks`,
                image: {
                    // Note: This URL must be public (hosted) for Discord to see it
                    url: `http://your-public-url.com/assets/icons/${item.files.icon}`
                }
            };

            message.channel.send({ embeds: [embed] });

        } catch (err) {
            console.error(err);
        }
    }
});
```
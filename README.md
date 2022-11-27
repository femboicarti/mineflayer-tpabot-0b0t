# mineflayer-tpabot-0b0t
A simple TPA Bot for 0b0t, using a few plugins for extra safety.
------------------------------------------------------------------
### Plugins: 
[PrismarineViewer](https://github.com/PrismarineJS/prismarine-viewer),
[AutoEat](https://github.com/link-discord/mineflayer-auto-eat),
[AutoTotem](https://github.com/SpaceEngineer0/mineflayer-autotem)
### Script:
```js
const mineflayer = require('mineflayer')
const mineflayerViewer = require('prismarine-viewer').mineflayer
const autoeat = require('mineflayer-auto-eat').default
const autotem = require('mineflayer-autotem')
let bot = mineflayer.createBot({
    version: "1.12.2",
    host: "0b0t.org",
    username: "x",
    // password: "x",
    // port: "25565",
    auth: 'microsoft'


    })



  function botstart() {
    const bot = mineflayer.createBot({
      version: "1.12.2",
      host: "0b0t.org",
      username: "x",
      // password: "x",
      // port: "25565",
      auth: 'microsoft'


    })}


  bot.on("end", function() {
    setTimeout(() => {
        botstart()
    }, 10000)
  })
  function antiAfk() {
    setTimeout(function() {
    bot.swingArm('right');
    antiAfk()
    }, 60000);
  }

  bot.on('spawn', () => {
   antiAfk() 
})

  
  bot.loadPlugin(autoeat)
  
  bot.on('autoeat_started', (item, offhand) => {
    console.log("Eating ${item.name} in ${offhand ? 'offhand' : 'hand'}")
  })
  
  bot.on('autoeat_error', (error) => {
    console.error(error)
  })
  
  bot.on('autoeat_finished', (item, offhand) => {
    console.log("Finished eating ${item.name} in ${offhand ? 'offhand' : 'hand'}")
  })

  bot.once('spawn', () => {
    mineflayerViewer(bot, { port: 3000, firstPerson: true }) // port is the minecraft server port, if first person is false, you get a bird's-eye view
    bot.autoEat.options.priority = 'hunger'
    bot.autoEat.options.startAt = 19
})

bot.loadPlugin(autotem);
    bot.autotem.equip();


   var whiteList = [
    `"UUID",` // Name, optional
];


 
  ///tpa accepts working
  bindEvents(bot);

  function bindEvents(bot) { 
      bot.on('message', msg => {
          var regex = "^([a-zA-Z0-9]{3,16}) wants to teleport to you.$";
          var found = msg.toString().match(regex);

          if (found != null) {
              var uuid =  bot.players[found[1]].uuid;
              if (whiteList.includes(uuid)) {
                  bot.chat("/tpy " + found[1])
              }
          }})}
```
Thanks to Pr1stak <3.

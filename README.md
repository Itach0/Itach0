const { Function, getBuffer } = require('../lib/')
const { generateWAMessage, proto } = require('@adiwajshing/baileys');
const image = 'https://i.imgur.com/AXtC7iH.jpeg' //MAIN IMAGE URL HERE
const logo = 'https://i.imgur.com/53kpmax.jpeg'

Function(
	{
		pattern: 'intro ?(.*)',
		fromMe: true,
		desc: 'Shows My Intro',
		type: 'misc',
	},   async (message, match) => {
        const jid = message.jid
        const number = message.client.user.jid
        const thumb = await getBuffer(image)
        const thumbnail = await getBuffer(logo)
        const options = {}
	options.contextInfo = {
		forwardingScore: 999, // change it to 999 for many times forwarded
		isForwarded: false,
	}
        // ADDED /* TO REMOVE LINK PREVIEW TYPE
        options.linkPreview = {
               renderLargerThumbnail: true,
               showAdAttribution: true,
               title: "ðððð ððð¥",
               body: "á´ÊÉªá´á´ Êá´Êá´ ð¦ !!",
               mediaType: 1,
               thumbnail: thumb,
               sourceUrl: "http://wa.me/918136962641?text=_áÊá´ÊÊá´+á´á´sá´+sá´Ê+ÊÉªÉ¢+Òá´É´+á´ Êá´+ðª_"
             }
        // ADDED */ TO REMOVE LINK PREVIEW TYPE
        options.quoted = {
            key: {
                fromMe: false,
                participant: "0@s.whatsapp.net",
                remoteJid: "status@broadcast"
            },
            message: {
			'contactMessage': {
				'displayName': `${message.pushName}`, //ADD `${message.client.user.name}` TO DISPLAY CLIENT USER NAME.
				'vcard': `BEGIN:VCARD\nVERSION:3.0\nN:XL;${message.client.user.name},;;;\nFN:${message.client.user.name},\nitem1.TEL;waid=${number.split('@')[0]}:${number.split('@')[0]}\nitem1.X-ABLabel:Ponsel\nEND:VCARD`,
				'jpegThumbnail': thumbnail
			}
            }
        }
        
let messages = await generateWAMessage(message.jid, { text: `0ÛªÛªà½´à½»ê¦½ê¦¼Ì·â¸â¹â¢âââââââââââââââ¡á­
â       *ã ð ð¬ ðð¡ð§ð¥ð¢ ã*
â *Name      :* itachi
â *Place       :* japan
â *Gender   :*  á´á´Êá´
â *Age          :* error
â *Phone     :* wa.m+2349030079824
â *IG ID        : undefined 
â *Status     :* single 
â°âââââêª¶ ÛªÛªà½´à½»ê¦½ê¦¼Ì·â¸ â â â â êª¶ ÛªÛªà½´à½»ê¦½ê¦¼Ì·â¸`}, {quoted: message.quoted || ''})

await message.client.forwardMessage(message.jid, await proto.WebMessageInfo.fromObject(messages), options)

    }
);

const { default: makeWASocket, useMultiFileAuthState } = require('@whiskeysockets/baileys')
const cron = require('node-cron')

async function startBot() {
    const { state, saveCreds } = await useMultiFileAuthState('auth')
    const sock = makeWASocket({
        auth: state,
        printQRInTerminal: true,
    })

    sock.ev.on('creds.update', saveCreds)

    const groupId = '1234567890-123456@g.us' // Ganti dengan ID grup WA kamu

    // Fungsi cek admin
    async function isAdmin(participant) {
        const metadata = await sock.groupMetadata(groupId)
        const user = metadata.participants.find(p => p.id === participant)
        return user?.admin !== null && user?.admin !== undefined
    }

    // Handle pesan masuk (manual open/close)
    sock.ev.on('messages.upsert', async ({ messages }) => {
        const msg = messages[0]
        if (!msg.message || !msg.key.remoteJid.includes('@g.us')) return

        const text = (msg.message.conversation || msg.message.extendedTextMessage?.text || '').toLowerCase()
        const sender = msg.key.participant || msg.key.remoteJid

        if (text === '.close group') {
            if (await isAdmin(sender)) {
                await sock.groupSettingUpdate(groupId, 'announcement')
                await sock.sendMessage(groupId, { text: 'Grup ditutup oleh admin. Hanya admin yang bisa mengirim pesan.' })
            } else {
                await sock.sendMessage(sender, { text: 'Kamu bukan admin, tidak bisa menutup grup.' })
            }
        } else if (text === '.open group') {
            if (await isAdmin(sender)) {
                await sock.groupSettingUpdate(groupId, 'not_announcement')
                await sock.sendMessage(groupId, { text: 'Grup dibuka oleh admin. Semua anggota bisa mengirim pesan.' })
            } else {
                await sock.sendMessage(sender, { text: 'Kamu bukan admin, tidak bisa membuka grup.' })
            }
        }
    })

    // Jadwal otomatis (sama seperti sebelumnya)
    cron.schedule('0 22 * * 1-5', async () => {
        await sock.groupSettingUpdate(groupId, 'announcement')
        await sock.sendMessage(groupId, { text: 'Grup ditutup otomatis (Senin-Jumat, 22:00). Hanya admin yang bisa kirim pesan.' })
        console.log('Grup ditutup (Senin-Jumat, 22:00)')
    })

    cron.schedule('0 6 * * 1-5', async () => {
        await sock.groupSettingUpdate(groupId, 'not_announcement')
        await sock.sendMessage(groupId, { text: 'Grup dibuka otomatis (Senin-Jumat, 06:00). Semua anggota bisa kirim pesan.' })
        console.log('Grup dibuka (Senin-Jumat, 06:00)')
    })

    cron.schedule('0 0 * * 6,0', async () => {
        await sock.groupSettingUpdate(groupId, 'announcement')
        await sock.sendMessage(groupId, { text: 'Grup ditutup otomatis (Sabtu-Minggu, 00:00). Hanya admin yang bisa kirim pesan.' })
        console.log('Grup ditutup (Sabtu-Minggu, 00:00)')
    })

    cron.schedule('0 6 * * 6,0', async () => {
        await sock.groupSettingUpdate(groupId, 'not_announcement')
        await sock.sendMessage(groupId, { text: 'Grup dibuka otomatis (Sabtu-Minggu, 06:00). Semua anggota bisa kirim pesan.' })
        console.log('Grup dibuka (Sabtu-Minggu, 06:00)')
    })
}

startBot()

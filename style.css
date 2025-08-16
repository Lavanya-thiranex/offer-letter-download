const { google } = require('googleapis');

app.post('/api/offer-letter', async (req, res) => {
    const { email } = req.body;
    
    try {
        const drive = google.drive({ version: 'v3', auth });
        
        // Search for files containing the email in name or specific folder
        const response = await drive.files.list({
            q: `name contains '${email}' and mimeType = 'application/pdf'`,
            fields: 'files(id, name)'
        });
        
        if (response.data.files.length > 0) {
            const fileId = response.data.files[0].id;
            const downloadUrl = `https://drive.google.com/uc?export=download&id=${fileId}`;
            res.json({ success: true, downloadUrl });
        } else {
            res.status(404).json({ success: false, message: 'Offer letter not found' });
        }
    } catch (error) {
        res.status(500).json({ success: false, message: 'Server error' });
    }
});

# 🔧 Troubleshooting Guide

## Common Issues & Solutions

### ❌ Issue: Webhook not receiving messages
**Solution:**
- Verify webhook URL is publicly accessible
- Check Meta Developer Dashboard → Webhook status
- Ensure you subscribed to `messages` field

### ❌ Issue: Authentication error downloading media
**Solution:**
- Create Bearer Token credential in n8n
- Use your WhatsApp Access Token as the token value
- Apply to both HTTP Request nodes (audio + image download)

### ❌ Issue: Groq API returning error
**Solution:**
- Verify Groq API key is correct
- Check file format (must be audio/ogg or audio/mp4)
- Ensure file size < 25MB

### ❌ Issue: AI Agent not using tools
**Solution:**
- Review System Prompt — make sure tools are mentioned
- Check tool descriptions in n8n
- Verify tool credentials are correctly configured

### ❌ Issue: Wrong message routing
**Solution:**
- Check Switch Node conditions
- Enable "Loose Type Validation"
- Verify field paths match your WhatsApp payload

### ❌ Issue: Memory mixing between users
**Solution:**
- Check Session Key in Memory node
- Must use: `{{ $('WhatsApp Trigger').item.json.messages[0].from }}`

---

## Still stuck?

📺 Watch the full tutorial: [https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3](https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3)
🌐 Professional help: [https://yousefautomates.pages.dev/](https://yousefautomates.pages.dev/)

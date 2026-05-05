# 📋 Setup Guide — WhatsApp AI Agent

## Step 1: Meta Developer Setup

1. Go to [Meta for Developers](https://developers.facebook.com)
2. Create a new App → Business type
3. Add WhatsApp product
4. Get your:
   - **Phone Number ID**
   - **WhatsApp Business Account ID**
   - **Temporary Access Token** (for testing)
   - **Permanent Token** (from Meta Business Suite)

## Step 2: n8n Setup

### Option A: n8n Cloud
- Sign up at [n8n.io](https://n8n.io)
- Free tier available

### Option B: Self-Hosted (Docker)
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

## Step 3: API Keys Required

| Service | Where to Get | Free Tier |
|---------|-------------|-----------|
| OpenAI | [platform.openai.com](https://platform.openai.com) | $5 credit |
| Groq | [console.groq.com](https://console.groq.com) | ✅ Free |
| SerpAPI | [serpapi.com](https://serpapi.com) | 100/month |

## Step 4: Google Sheets Structure

Your contacts sheet should have these columns:
```
| Name          | Email                    |
|---------------|--------------------------|
| Ahmed Mohamed | ahmed@example.com        |
| Sara Ali      | sara@example.com         |
```

## Step 5: Environment Variables

In n8n → Settings → Variables:
```
phone = 201234567890
```
> ⚠️ Use international format without + sign

## Step 6: Webhook Configuration

In Meta Developer Dashboard:
- Webhook URL: `https://your-n8n-url/webhook/YOUR_WEBHOOK_ID`
- Verify Token: (any string you choose)
- Subscribe to: **messages**

## Troubleshooting

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues.

---
📺 Full video walkthrough: [https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3](https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3)

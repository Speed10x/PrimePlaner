# Premium Telegram Bot Setup Guide

A comprehensive Telegram bot for premium membership with payment verification, broadcasting, and admin features.

## 🚀 Features

- **Premium Membership System**: Lifetime access with payment verification
- **UPI Payment Integration**: QR code and manual verification
- **Admin Panel**: Complete bot management
- **Broadcasting System**: Send messages to all users
- **Auto Reminders**: Monthly promotional messages
- **User Management**: Profile system, premium tracking
- **Multi-Platform Hosting**: Supports Koyeb, Render, Heroku
- **Logging System**: Channel-based activity logging
- **Restart Command**: Remote bot restart

## 📁 Project Structure

```
premium-telegram-bot/
├── main.py              # Main bot application
├── requirements.txt     # Python dependencies
├── Dockerfile          # Docker configuration
├── Procfile            # Heroku process file
├── runtime.txt         # Python version
├── koyeb.yaml         # Koyeb deployment config
├── render.yaml        # Render deployment config
├── .env.example       # Environment variables template
├── SETUP_GUIDE.md     # This setup guide
└── README.md          # Project documentation
```

## 🛠️ Prerequisites

1. **Telegram Bot Token**: Get from [@BotFather](https://t.me/botfather)
2. **Premium Channel**: Create a private channel for premium content
3. **Log Channel**: Create a channel for bot logs
4. **UPI Account**: For payment collection
5. **Hosting Account**: Koyeb, Render, or Heroku

## 📝 Initial Setup

### 1. Create Telegram Bot

1. Message [@BotFather](https://t.me/botfather)
2. Send `/newbot`
3. Choose bot name and username
4. Save the bot token

### 2. Setup Channels

**Premium Channel:**
1. Create a private channel
2. Add your bot as admin
3. Get channel invite link
4. Note the channel ID

**Log Channel:**
1. Create a channel for logs
2. Add your bot as admin
3. Note the channel ID (starts with -100)

### 3. Get User IDs

1. Message [@userinfobot](https://t.me/userinfobot)
2. Get your user ID for admin access

## 🔧 Environment Configuration

Create `.env` file from `.env.example`:

```bash
# Bot Configuration
BOT_TOKEN=5678901234:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw
ADMIN_IDS=123456789,987654321
LOG_CHANNEL=-1001234567890

# Payment Configuration
UPI_ID=yourname@paytm
PAYMENT_AMOUNT=70

# Premium Channel Configuration
PREMIUM_CHANNEL_ID=-1001234567890
PREMIUM_CHANNEL_LINK=https://t.me/+AbCdEfGhIjKlMnOp

# Database Configuration
DATABASE_URL=bot_database.db

# Hosting Configuration
PORT=8000
HOST=0.0.0.0
WEBHOOK_URL=https://your-app-name.koyeb.app
```

## 🚀 Deployment Options

### Option 1: Koyeb Deployment

1. **Fork/Clone Repository**
   ```bash
   git clone <your-repo-url>
   cd premium-telegram-bot
   ```

2. **Create Koyeb Account**
   - Visit [koyeb.com](https://www.koyeb.com)
   - Sign up with GitHub

3. **Deploy from GitHub**
   - Connect your GitHub repository
   - Set environment variables in Koyeb dashboard
   - Deploy using `koyeb.yaml` configuration

4. **Set Webhook URL**
   ```bash
   WEBHOOK_URL=https://your-app-name.koyeb.app
   ```

### Option 2: Render Deployment

1. **Create Render Account**
   - Visit [render.com](https://render.com)
   - Connect GitHub account

2. **Create Web Service**
   - Select your repository
   - Use `render.yaml` configuration
   - Set environment variables

3. **Configure Environment**
   - Add all variables from `.env.example`
   - Set `WEBHOOK_URL` to your Render URL

### Option 3: Heroku Deployment

1. **Install Heroku CLI**
   ```bash
   # Install Heroku CLI
   curl https://cli-assets.heroku.com/install.sh | sh
   ```

2. **Deploy to Heroku**
   ```bash
   # Login to Heroku
   heroku login

   # Create app
   heroku create your-bot-name

   # Set environment variables
   heroku config:set BOT_TOKEN=your_token
   heroku config:set ADMIN_IDS=123456789
   heroku config:set LOG_CHANNEL=-1001234567890
   # ... set all other variables

   # Deploy
   git push heroku main
   ```

### Option 4: Local Development

1. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Setup Environment**
   ```bash
   cp .env.example .env
   # Edit .env with your values
   # Leave WEBHOOK_URL empty for local development
   ```

3. **Run Bot**
   ```bash
   python main.py
   ```

## 🎛️ Bot Commands

### User Commands
- `/start` - Start the bot and show main menu
- `/profile` - View user profile and premium status

### Admin Commands
- `/admin` - Access admin panel with statistics
- `/broadcast <message>` - Send message to all users
- `/restart` - Restart the bot (admin only)

## 🎮 Usage Instructions

### For Users

1. **Start Bot**: Send `/start`
2. **Buy Premium**: Click "Buy Premium" button
3. **Make Payment**: Pay via UPI using provided details
4. **Upload Screenshot**: Send payment screenshot
5. **Wait for Verification**: Admin will verify and grant access

### For Admins

1. **View Stats**: Use `/admin` command
2. **Verify Payments**: Check pending payments in admin panel
3. **Broadcast Messages**: Use `/broadcast` command
4. **Monitor Logs**: Check log channel for activities

## 🔧 Configuration Options

### Payment Settings
- `PAYMENT_AMOUNT`: Premium membership price
- `UPI_ID`: Your UPI ID for payments

### Channel Settings
- `PREMIUM_CHANNEL_ID`: Your premium channel ID
- `PREMIUM_CHANNEL_LINK`: Invite link to premium channel
- `LOG_CHANNEL`: Channel for bot activity logs

### Admin Settings
- `ADMIN_IDS`: Comma-separated admin user IDs
- Multiple admins supported

## 📊 Database Schema

The bot automatically creates SQLite database with tables:
- `users`: User information and premium status
- `payments`: Payment records and verification status
- `admins`: Admin user management
- `broadcasts`: Broadcast message history

## 🛡️ Security Features

- Admin-only commands protection
- Payment verification system
- User activity logging
- Anti-spam measures
- Secure database handling

## 🔄 Automated Features

### Daily Tasks (9 AM)
- Check expired premium memberships
- Send renewal notifications

### Monthly Tasks (1st of month)
- Send promotional messages to free users
- Marketing reminders

## 🐛 Troubleshooting

### Common Issues

1. **Bot Not Responding**
   - Check BOT_TOKEN is correct
   - Verify bot is not stopped by Telegram
   - Check hosting service logs

2. **Payment Verification Not Working**
   - Ensure admin IDs are correct
   - Check if admin has started the bot
   - Verify channel permissions

3. **Database Errors**
   - Check file permissions
   - Ensure database directory exists
   - Verify DATABASE_URL path

4. **Webhook Issues**
   - Ensure WEBHOOK_URL is accessible
   - Check SSL certificate validity
   - Verify port configuration

### Debug Mode

For development, set logging level:
```python
logging.basicConfig(level=logging.DEBUG)
```

## 📈 Scaling Considerations

- **Database**: Consider PostgreSQL for high traffic
- **File Storage**: Use cloud storage for payment screenshots
- **Rate Limiting**: Implement advanced rate limiting for broadcasts
- **Monitoring**: Add health check endpoints
- **Backup**: Regular database backups

## 🔒 Production Checklist

- [ ] Secure environment variables
- [ ] Enable SSL/HTTPS
- [ ] Configure database backups
- [ ] Set up monitoring alerts
- [ ] Test all payment flows
- [ ] Verify admin functions
- [ ] Test broadcast limits
- [ ] Configure log retention

## 📞 Support

For issues and questions:
1. Check troubleshooting section
2. Review hosting platform logs
3. Test with `/start` command
4. Verify all environment variables

## 🚀 Advanced Features

### Custom Extensions
- Add more payment methods
- Implement referral system
- Create subscription tiers
- Add analytics dashboard

### Integration Options
- Webhook notifications
- External payment gateways
- CRM integration
- Analytics platforms

---

## 🎉 Congratulations!

Your premium Telegram bot is now ready! Users can:
- ✅ Purchase premium membership
- ✅ Upload payment screenshots  
- ✅ Get instant verification
- ✅ Access premium content
- ✅ Receive automated reminders

Admins can:
- ✅ Manage all users
- ✅ Verify payments
- ✅ Broadcast messages
- ✅ Monitor activities
- ✅ Restart bot remotely

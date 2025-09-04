# 🤖 Premium Telegram Bot

A feature-rich Telegram bot for premium membership management with payment verification, broadcasting, and comprehensive admin tools.

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://python.org)
[![Telegram Bot API](https://img.shields.io/badge/Telegram%20Bot%20API-Latest-blue.svg)](https://core.telegram.org/bots/api)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## ✨ Features

### 🔥 Core Features
- **Premium Membership System** - Lifetime access with payment verification
- **UPI Payment Integration** - QR code generation and manual verification
- **Multi-Admin Support** - Multiple admins with permission management
- **Broadcasting System** - Send messages to all users with delivery tracking
- **User Management** - Complete user profile and premium status tracking
- **Auto Reminders** - Monthly promotional messages and renewal notifications

### 🎛️ Admin Features  
- **Real-time Statistics** - User counts, premium members, payment analytics
- **Payment Verification** - Manual payment approval with screenshot review
- **User Blocking/Unblocking** - Admin user management
- **Broadcast Analytics** - Track message delivery success/failure
- **Activity Logging** - Channel-based comprehensive logging
- **Remote Restart** - Restart bot without server access

### 🚀 Technical Features
- **Multi-Platform Hosting** - Supports Koyeb, Render, Heroku
- **Webhook & Polling** - Automatic mode detection
- **Database Management** - SQLite with easy migration to PostgreSQL  
- **Scheduled Tasks** - Automated premium expiry and reminder system
- **Error Handling** - Comprehensive error logging and recovery
- **Rate Limiting** - Built-in spam protection

## 🖼️ Screenshots

### User Interface
- Clean, modern inline keyboard design
- Payment QR code generation
- Premium status dashboard
- Support contact system

### Admin Panel
- Comprehensive statistics dashboard
- Payment verification interface
- Broadcasting system
- User management tools

## 🛠️ Quick Setup

### 1. Prerequisites
```bash
# Required
- Telegram Bot Token (from @BotFather)
- Admin Telegram User ID
- Premium Channel (private)
- UPI Account for payments

# Optional  
- Log Channel for activity tracking
- Custom payment amount
```

### 2. Environment Setup
```bash
# Clone repository
git clone <your-repo-url>
cd premium-telegram-bot

# Copy environment template
cp .env.example .env

# Edit with your details
nano .env
```

### 3. Deploy Options

#### 🚀 Koyeb (Recommended)
```bash
# Connect GitHub repository to Koyeb
# Set environment variables in dashboard
# Deploy automatically with koyeb.yaml
```

#### 🌐 Render
```bash
# Create new Web Service from GitHub
# Configure environment variables
# Deploy with render.yaml
```

#### 📦 Heroku
```bash
heroku create your-bot-name
heroku config:set BOT_TOKEN=your_token
# ... set other variables
git push heroku main
```

#### 💻 Local Development
```bash
pip install -r requirements.txt
python main.py
```

## 📋 Environment Variables

```bash
# Essential Configuration
BOT_TOKEN=your_bot_token_from_botfather
ADMIN_IDS=123456789,987654321  # Comma-separated
LOG_CHANNEL=-1001234567890     # Optional

# Payment Settings
UPI_ID=yourname@paytm
PAYMENT_AMOUNT=70

# Premium Channel
PREMIUM_CHANNEL_ID=-1001234567890
PREMIUM_CHANNEL_LINK=https://t.me/+your_invite_link

# Hosting (Production Only)
WEBHOOK_URL=https://your-app.koyeb.app
PORT=8000
HOST=0.0.0.0
```

## 🎮 Usage

### User Commands
```bash
/start     # Start bot and show main menu
/profile   # View profile and premium status
```

### Admin Commands  
```bash
/admin       # Access admin dashboard
/broadcast   # Send message to all users
/restart     # Restart bot remotely
```

### User Flow
1. **Start** → Send `/start` command
2. **Buy Premium** → Click "Buy Premium" button  
3. **Pay** → Use UPI with provided details
4. **Screenshot** → Upload payment screenshot
5. **Verification** → Wait for admin approval
6. **Access** → Get premium channel link

### Admin Flow
1. **Monitor** → Use `/admin` for statistics
2. **Verify** → Review payment screenshots
3. **Approve** → Grant premium access
4. **Broadcast** → Send announcements
5. **Manage** → Block/unblock users

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────┐    ┌─────────────┐
│   Telegram API  │────│  Bot Server  │────│  Database   │
└─────────────────┘    └──────────────┘    └─────────────┘
                              │
                    ┌─────────┼─────────┐
                    │         │         │
              ┌─────▼──┐ ┌────▼───┐ ┌──▼────┐
              │Webhook │ │Scheduler│ │Logging│
              └────────┘ └────────┘ └───────┘
```

### Database Schema
- **users**: User profiles and premium status
- **payments**: Payment records and verification
- **admins**: Admin permissions and activity  
- **broadcasts**: Message history and analytics

## 📊 Features in Detail

### Payment System
- **QR Code Generation**: Automatic UPI QR codes
- **Manual Verification**: Admin screenshot review
- **Status Tracking**: Pending, verified, rejected states
- **Notification System**: User and admin alerts

### Broadcasting
- **Targeted Messaging**: All users, premium only, or free users
- **Delivery Tracking**: Success/failure statistics
- **Rate Limiting**: Spam prevention
- **Message Scheduling**: Future message delivery

### User Management  
- **Profile System**: Join date, activity tracking
- **Premium Tracking**: Expiry dates, renewal reminders
- **Activity Monitoring**: Last active timestamps
- **Blocking System**: Admin user control

## 🔧 Customization

### Adding New Features
```python
# Add new command handler
async def new_command_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    # Your custom logic here
    pass

# Register handler
application.add_handler(CommandHandler("newcommand", new_command_handler))
```

### Database Extensions
```python
# Add new table
cursor.execute('''
    CREATE TABLE IF NOT EXISTS new_table (
        id INTEGER PRIMARY KEY,
        data TEXT
    )
''')
```

### Custom Payment Methods
```python
# Extend payment verification
def verify_custom_payment(payment_data):
    # Custom verification logic
    return True/False
```

## 📈 Analytics & Monitoring

### Built-in Analytics
- User growth tracking
- Payment conversion rates  
- Premium membership analytics
- Broadcast engagement metrics

### Logging System
- Channel-based activity logs
- Error tracking and alerts
- Performance monitoring
- Security event logging

## 🔒 Security Features

- **Admin Authentication**: Multi-level admin permissions
- **Payment Verification**: Manual screenshot review
- **Rate Limiting**: Anti-spam protection
- **Data Encryption**: Secure database storage
- **Access Control**: Channel-based permissions

## 🚀 Performance Optimization

### Database Optimization
- Indexed queries for fast lookups
- Connection pooling
- Automatic cleanup of old data
- Migration support for scaling

### Memory Management
- Efficient state management
- Garbage collection optimization
- Resource cleanup
- Connection management

## 📞 Support & Troubleshooting

### Common Issues
1. **Bot not responding** → Check token and permissions
2. **Payments not working** → Verify admin setup
3. **Broadcasting fails** → Check rate limits
4. **Database errors** → Verify file permissions

### Debug Mode
```python
# Enable debug logging
logging.basicConfig(level=logging.DEBUG)
```

### Health Checks
```bash
# Test bot connectivity
curl https://api.telegram.org/bot{TOKEN}/getMe

# Check webhook status  
curl https://api.telegram.org/bot{TOKEN}/getWebhookInfo
```

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) - Telegram Bot API wrapper
- [Telegram Bot API](https://core.telegram.org/bots/api) - Official API documentation
- [Koyeb](https://www.koyeb.com) - Hosting platform

##

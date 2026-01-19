# NGO Registration and Donation Management System

A comprehensive web application for managing NGO registrations and processing donations with integrated payment gateway support. Built with Node.js, Express, MongoDB, and PayHere payment integration.

## 🎯 Features

### User Features
- *User Registration & Authentication*: Secure user registration and login system with password hashing
- *Donation Management*: Users can make donations through integrated PayHere payment gateway
- *Personal Dashboard*: View donation history, transaction status, and account information
- *PDF Receipt Generation*: Download official donation receipts as PDF files
- *Profile Settings*: Update profile information and change password

### Admin Features
- *Admin Dashboard*: Comprehensive dashboard with statistics and analytics
- *User Management*: View all registered users, filter by role, and manage user accounts
- *Donation Tracking*: Monitor all donations with filtering and sorting capabilities
- *Real-time Notifications*: Get notified about new user registrations and donations
- *Analytics & Charts*: Visual representation of donation trends (last 7 days and last 30 days)
- *Export Functionality*: Export user data to CSV format
- *PDF Reports*: Generate comprehensive donation reports in PDF format

### Superadmin Features
- *Role Management*: Promote users to admin role or remove admin privileges
- *Full System Access*: Complete control over the system

## 🛠️ Technologies Used

- *Backend*: Node.js, Express.js
- *Database*: MongoDB (MongoDB Atlas)
- *Template Engine*: EJS
- *Authentication*: Express Sessions, bcryptjs
- *Payment Gateway*: PayHere (Sri Lanka)
- *PDF Generation*: PDFKit
- *Security*: MD5 hashing for payment verification

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v14 or higher)
- npm (Node Package Manager)
- MongoDB Atlas account (or local MongoDB instance)
- PayHere merchant account (for payment processing)

## 🚀 Installation

1. *Clone the repository*
   bash
   git clone https://github.com/amaan-ee-iitr/NGO-Registration-and-Donation-Management-System
   cd NGO-Registration-and-Donation-Management-System
   

2. *Install dependencies*
   bash
   npm install
   

3. *Create a .env file* in the root directory with the following variables:
   env
   MONGO_URI=your_mongodb_connection_string
   SESSION_SECRET=your_secret_key
   PAYHERE_MERCHANT_ID=your_payhere_merchant_id
   PAYHERE_MERCHANT_SECRET=your_payhere_merchant_secret
   PORT=3000

4. *Start the server*
   bash
   node server.js
   
   
   Or with nodemon (for development):
   bash
   nodemon server.js
   

5. *Access the application*
   - Open your browser and navigate to http://localhost:3000

## ⚙️ Configuration

### Environment Variables

Create a .env file in the root directory with the following required variables:

- MONGO_URI: MongoDB connection string (e.g., mongodb+srv://username:password@cluster.mongodb.net/dbname)
- PAYHERE_MERCHANT_ID: Your PayHere merchant ID
- PAYHERE_MERCHANT_SECRET: Your PayHere merchant secret key

### PayHere Integration

The application uses PayHere payment gateway for processing donations. Make sure to:
1. Sign up for a PayHere merchant account
2. Configure your return URL: http://your-domain.com/payment/success
3. Configure your notify URL (webhook): http://your-domain.com/payment/notify
4. Use sandbox mode for testing (set sandbox: true in payment configuration)

## 📁 Project Structure


NGO-Registration-and-Donation-Management-System-main/
│
├── public/
│   └── images/
│       └── nss-logo.jpg          # Organization logo
│
├── views/
│   ├── index.ejs                 # Home page
│   ├── login.ejs                 # Login page
│   ├── register.ejs              # Registration page
│   ├── dashboard.ejs              # User dashboard
│   ├── admin.ejs                 # Admin dashboard
│   ├── settings.ejs               # User settings page
│   └── payment_gateway.ejs        # Payment gateway page
│
├── server.js                      # Main server file
├── package.json                   # Dependencies and scripts
├── .env                          # Environment variables (create this)
└── README.md                      # Project documentation


## 🔐 User Roles

The system supports three user roles:

1. *User*: Default role for registered users
   - Can make donations
   - View personal donation history
   - Download receipts
   - Update profile settings

2. *Admin*: Can be assigned by superadmin
   - All user privileges
   - Access to admin dashboard
   - View all users and donations
   - Generate reports and exports
   - View notifications

3. *Superadmin*: Highest privilege level
   - All admin privileges
   - Can promote users to admin
   - Can remove admin privileges

## 📡 API Endpoints

### Authentication Routes
- GET / - Home page
- GET /register - Registration page
- POST /register - Register new user
- GET /login - Login page
- POST /login - User login
- GET /logout - User logout

### User Routes
- GET /dashboard - User dashboard (requires login)
- GET /settings - User settings page (requires login)
- POST /settings - Update user settings (requires login)
- GET /receipt/:id - Download donation receipt PDF (requires login)

### Payment Routes
- POST /get-hash - Generate payment hash for PayHere (requires login)
- GET /payment/success - Payment success callback
- POST /payment/notify - Payment webhook notification

### Admin Routes
- GET /admin - Admin dashboard (requires admin role)
- GET /admin/clear-notifications - Clear notifications (requires admin)
- GET /admin/report-pdf - Generate donation report PDF (requires admin)
- GET /admin/export - Export users to CSV (requires admin)

### Superadmin Routes
- POST /superadmin/make-admin/:id - Promote user to admin (requires superadmin)
- POST /superadmin/remove-admin/:id - Remove admin privileges (requires superadmin)

## 💳 Payment Flow

1. User enters donation amount on dashboard
2. Frontend requests secure hash from backend (/get-hash)
3. Backend generates MD5 hash using PayHere algorithm
4. Payment object is created with hash and payment details
5. PayHere popup is opened for payment processing
6. On successful payment:
   - PayHere redirects to /payment/success
   - Webhook notification sent to /payment/notify
   - Donation status updated to 'success'
   - Notification created for admin

## 🔒 Security Features

- Password hashing using bcryptjs
- Session-based authentication
- Role-based access control (RBAC)
- MD5 hash verification for payment security
- Protected routes with middleware
- Input validation and sanitization

## 📊 Database Models

### User Schema
- name: String
- email: String (unique, required)
- password: String (hashed, required)
- role: String (enum: 'user', 'admin', 'superadmin')
- registeredAt: Date

### Donation Schema
- userId: ObjectId (reference to User)
- amount: Number
- status: String (default: 'pending')
- transactionId: String
- orderId: String
- date: Date

### Notification Schema
- message: String
- type: String ('success' or 'info')
- date: Date

## 🎨 Features in Detail

### Admin Dashboard
- *Statistics*: Total donations, user counts, donation trends
- *Charts*: Visual analytics for last 7 days and last 30 days
- *User Management*: Filter users by role, view all registered users
- *Donation Management*: Sort donations by date or amount
- *Notifications*: Real-time notifications for new users and donations
- *Export*: Download user list as CSV
- *Reports*: Generate comprehensive PDF reports

### User Dashboard
- *Donation Form*: Enter amount and make donations
- *Donation History*: View all past donations with status
- *Receipt Download*: Download PDF receipts for successful donations
- *Profile Access*: Quick link to settings page

## 🐛 Troubleshooting

### Common Issues

1. *MongoDB Connection Error*
   - Verify your MONGO_URI in .env file
   - Check if MongoDB Atlas IP whitelist includes your IP
   - Ensure network connectivity

2. *PayHere Payment Issues*
   - Verify merchant ID and secret in .env
   - Check if using sandbox mode for testing
   - Ensure return URL and notify URL are correctly configured

3. *Session Issues*
   - Clear browser cookies and try again
   - Check if session secret is set correctly

## 📝 Development

### Running in Development Mode

Install nodemon globally:
bash
npm install -g nodemon


Run with auto-reload:
bash
nodemon server.js


## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the ISC License.

## 👤 Author

NGO Registration and Donation Management System

## 🙏 Acknowledgments

- PayHere for payment gateway integration
- MongoDB Atlas for database hosting
- Express.js community for excellent documentation

---

*Note*: Make sure to keep your .env file secure and never commit it to version control. Add .env to your .gitignore file.

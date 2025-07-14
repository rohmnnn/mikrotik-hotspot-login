# MikroTik Hotspot Login Template

A modern, responsive hotspot login template for MikroTik RouterOS with a futuristic design and multiple theme options.

## 🌟 Features

- **Modern UI/UX**: Futuristic design with glass-morphism effects
- **Responsive Design**: Works perfectly on desktop, tablet, and mobile devices
- **Multiple Themes**: Green (default), Light, and Dark themes available
- **Multi-language Support**: Currently supports Indonesian language
- **Security**: CHAP authentication support with MD5 hashing
- **Free Access**: Built-in "Free WhatsApp" access button
- **Status Page**: Real-time connection status and usage monitoring
- **Error Handling**: Comprehensive error pages with user-friendly messages

## 📸 Screenshots

### Login Page
![Login Page](https://raw.githubusercontent.com/rohmnnn/mikrotik-hotspot-login/refs/heads/main/img/login.jpeg)

### Status Page (Connected User)
![Status Page](https://raw.githubusercontent.com/rohmnnn/mikrotik-hotspot-login/refs/heads/main/img/status.jpeg)

### Logout Page (Session Summary)
![Logout Page](https://raw.githubusercontent.com/rohmnnn/mikrotik-hotspot-login/refs/heads/main/img/logout.jpeg)

### Design Features Showcase
- **Glowing Border Effects**: Dynamic green glow animation around login cards
- **Glass-morphism**: Semi-transparent cards with backdrop blur effects
- **Responsive Layout**: Centered design that works on all screen sizes
- **Modern Typography**: Clean, readable fonts with proper contrast
- **Futuristic Theme**: Dark gradient background with cyan/green accent colors

## 📁 File Structure

```
├── login.html          # Main login page
├── status.html         # User status/dashboard page
├── logout.html         # Logout confirmation page
├── error.html          # Error page
├── alogin.html         # Advertisement login page
├── rlogin.html         # Redirect login page
├── redirect.html       # Redirect handler
├── radvert.html        # Advertisement redirect
├── md5.js             # MD5 hashing library for CHAP
├── api.json           # API configuration
├── favicon.ico        # Site favicon
├── css/
│   └── style.css      # Main stylesheet with all themes
├── img/
│   ├── user.svg       # User icon
│   └── password.svg   # Password icon
└── xml/               # XML templates for WISP compliance
    ├── login.html
    ├── logout.html
    ├── error.html
    ├── alogin.html
    ├── flogout.html
    ├── rlogin.html
    └── WISPAccessGatewayParam.xsd
```

## 🚀 Installation

### Method 1: FTP Upload (Recommended)

1. **Connect to your MikroTik router via FTP:**
   ```bash
   # Using any FTP client
   Host: [your-router-ip]
   Username: [admin-username]
   Password: [admin-password]
   Port: 21
   ```

2. **Upload all files to the hotspot directory:**
   - Upload all HTML files to the root of the hotspot folder
   - Upload `css/` folder with `style.css`
   - Upload `img/` folder with SVG icons
   - Upload `xml/` folder (optional, for WISP compliance)
   - Upload `md5.js` file

### Method 2: Winbox File Manager

1. Open Winbox and connect to your router
2. Go to **Files** menu
3. Navigate to the **hotspot** folder
4. Drag and drop all template files
5. Ensure proper folder structure is maintained

### Method 3: Terminal Upload

1. Connect via SSH/Telnet to your router
2. Use the following commands:
   ```mikrotik
   /file
   upload
   # Then drag files to the terminal or use TFTP
   ```

## ⚙️ Configuration

### 1. Enable Hotspot Service

```mikrotik
# Create hotspot server
/ip hotspot setup
# Follow the setup wizard

# Or configure manually:
/ip hotspot
add name=hotspot1 interface=wlan1 address-pool=hs-pool-1 profile=hsprof1
```

### 2. Configure Hotspot Profile

```mikrotik
/ip hotspot profile
set hsprof1 html-directory=hotspot login-by=username,http-chap dns-name=""
```

### 3. Set Up User Authentication

#### For database users:
```mikrotik
/ip hotspot user
add name=user1 password=pass1 profile=default
```

#### For RADIUS authentication:
```mikrotik
/radius
add service=hotspot address=192.168.1.100 secret=sharedsecret

/ip hotspot profile
set hsprof1 use-radius=yes
```

### 4. Configure Walled Garden (Optional)

Allow access to specific sites without authentication:

```mikrotik
/ip hotspot walled-garden
add dst-host=*.facebook.com
add dst-host=*.whatsapp.com
add dst-host=*.google.com
```

## 🎨 Theme Customization

The template includes three built-in themes. To change themes, modify the `<body>` tag class in the HTML files:

### Green Theme (Default)
```html
<body class="green-theme">
```

### Light Theme
```html
<body class="lite">
```

### Dark Theme
```html
<body class="dark">
```

### Custom Theme Colors

You can customize colors by editing `css/style.css`. Key color variables for each theme:

#### Green Theme
```css
/* Primary colors */
--primary: #00ffb0;
--secondary: #00e0ff;
--background: linear-gradient(120deg, #232526 0%, #414345 100%);
```

#### Light Theme
```css
/* Primary colors */
--primary: #007bff;
--secondary: #6c757d;
--background: #f8f9fa;
```

#### Dark Theme
```css
/* Primary colors */
--primary: #bb86fc;
--secondary: #03dac6;
--background: #121212;
```

## 🌐 Language Customization

To customize the language, edit the text in the HTML files:

### Common Text Elements

| Element | Location | Current Text (ID) | Change To |
|---------|----------|-------------------|-----------|
| Title | `login.html` | "Internet hotspot - Log in" | Your text |
| Header | `login.html` | "WIFI" | Your text |
| Subtitle | `login.html` | "Masuk untuk mengakses internet" | Your text |
| Username | `login.html` | "Nama Pengguna" | "Username" |
| Password | `login.html` | "Kata Sandi" | "Password" |
| Connect Button | `login.html` | "Sambungkan" | "Connect" |
| Free WA Button | `login.html` | "Paket WA Gratis" | "Free WhatsApp" |

### Example English Translation

```html
<!-- In login.html -->
<h1>WIFI</h1>
<p class="subtitle">Sign in to access internet</p>

<!-- Form labels -->
<input name="username" placeholder="Username" />
<label for="username">Username</label>

<input name="password" placeholder="Password" />
<label for="password">Password</label>

<button type="submit">Connect</button>
<button type="button" onclick="waLogin()">Free WhatsApp</button>
```

## 🔧 Advanced Configuration

### 1. Enable HTTPS (SSL)

```mikrotik
/ip hotspot profile
set hsprof1 http-cookie-lifetime=1d use-radius=yes hotspot-address=10.5.50.1 \
    dns-name="hotspot.example.com" http-proxy=0.0.0.0:0 https-redirect=yes
```

### 2. Custom Terms of Service

Add terms of service by modifying `login.html`:

```html
<div class="terms">
    <input type="checkbox" id="terms" required>
    <label for="terms">I agree to the <a href="/terms.html">Terms of Service</a></label>
</div>
```

### 3. Social Media Login Integration

Add social login buttons (requires external authentication):

```html
<div class="social-login">
    <button type="button" class="btn-facebook">Login with Facebook</button>
    <button type="button" class="btn-google">Login with Google</button>
</div>
```

### 4. Bandwidth Monitoring

Enhance the status page with real-time bandwidth monitoring by adding JavaScript:

```javascript
// Add to status.html
function updateStats() {
    // Refresh page every 30 seconds to update stats
    setTimeout(function() {
        window.location.reload();
    }, 30000);
}
```

## 📱 Mobile Optimization

The template is fully responsive. Key features for mobile:

- **Touch-friendly buttons**: Large tap targets
- **Responsive typography**: Scales with screen size
- **Gesture support**: Swipe and touch interactions
- **Fast loading**: Optimized CSS and minimal JavaScript

### Mobile-specific CSS

```css
@media (max-width: 768px) {
    .login-card {
        margin: 20px;
        padding: 30px 20px;
    }
    
    .login-header h1 {
        font-size: 1.8rem;
    }
}
```

## 🛠️ Troubleshooting

### Common Issues

#### 1. Template Not Loading
**Problem**: Default MikroTik login page shows instead of custom template.

**Solution**:
- Check file upload was successful
- Verify hotspot profile is set to use correct html-directory
- Ensure files are in the root of hotspot directory

```mikrotik
/ip hotspot profile print
/ip hotspot profile set [profile-name] html-directory=hotspot
```

#### 2. Styling Not Applied
**Problem**: Page loads but without custom styling.

**Solution**:
- Check `css/style.css` file is uploaded
- Verify folder structure is correct
- Clear browser cache

#### 3. Authentication Issues
**Problem**: Login fails even with correct credentials.

**Solution**:
- Check user database: `/ip hotspot user print`
- Verify RADIUS server (if used): `/radius monitor 0`
- Check hotspot profile settings

#### 4. Mobile Display Issues
**Problem**: Template doesn't display correctly on mobile.

**Solution**:
- Ensure viewport meta tag is present
- Check responsive CSS is loading
- Test on different devices

### Debug Commands

```mikrotik
# Check hotspot status
/ip hotspot print

# Monitor hotspot connections
/ip hotspot active print

# Check user database
/ip hotspot user print

# Monitor RADIUS (if used)
/radius monitor 0

# Check file system
/file print where name~"hotspot"
```

## 🔒 Security Best Practices

### 1. Change Default Credentials
```mikrotik
/user set admin password=new-strong-password
```

### 2. Enable HTTPS
```mikrotik
/ip hotspot profile set hsprof1 https-redirect=yes
```

### 3. Configure Firewall Rules
```mikrotik
/ip firewall filter
add chain=input action=accept protocol=tcp dst-port=80,443,8080,8291 comment="Allow web access"
add chain=input action=drop comment="Drop all other input"
```

### 4. Regular Updates
- Keep RouterOS updated
- Monitor security advisories
- Regular backup of configuration

## 📊 Performance Optimization

### 1. Enable Caching
```mikrotik
/ip proxy set enabled=yes port=8080 cache-administrator=admin@example.com
```

### 2. Optimize CSS/JS
- Minify CSS files
- Optimize images
- Use CDN for external resources

### 3. Database Optimization
```mikrotik
# Clean old user sessions
/ip hotspot active remove [find]

# Optimize user database
/system script run hotspot-cleanup
```

## 🤝 Contributing

Feel free to contribute to this template by:

1. **Reporting bugs**: Open an issue with detailed description
2. **Suggesting features**: Propose new functionality
3. **Submitting translations**: Add support for new languages
4. **Improving design**: Enhance UI/UX elements

## 📄 License

This template is provided as-is for educational and commercial use. Feel free to modify and distribute.

## 🆘 Support

For support and questions:

1. **MikroTik Documentation**: [https://help.mikrotik.com/](https://help.mikrotik.com/)
2. **Community Forum**: [https://forum.mikrotik.com/](https://forum.mikrotik.com/)
3. **RouterOS Manual**: [https://wiki.mikrotik.com/](https://wiki.mikrotik.com/)

## 📈 Changelog

### v1.0.0
- Initial release with modern UI design
- Multiple theme support
- Responsive design
- CHAP authentication support
- Indonesian language interface

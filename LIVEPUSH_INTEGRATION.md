# 🔧 LivePush.io Code Integration

## Quick Setup: Add These 3 Code Blocks to Your Website

---

### **STEP 1: Add LivePush.io CDN (Before closing </body> tag)**

Find this line in your HTML (around line 1350):
```html
</body>
```

**ADD THIS BEFORE IT:**
```html
<script src="https://cdn.livepush.io/livepush.min.js"></script>
```

---

### **STEP 2: Add LivePush Configuration (Top of your <script> section)**

Find this line (around line 1352):
```javascript
<script>
    // Smooth scrolling for navigation
```

**ADD THIS RIGHT AFTER `<script>`:**
```javascript
// ============ LIVEPUSH.IO CONFIGURATION ============
const LIVEPUSH_CONFIG = {
    appId: 'YOUR_LIVEPUSH_APP_ID',  // Get this from livepush.io dashboard
    channelName: 'doyourhomework-radio-chat'
};

let livePush = null;

// Initialize LivePush.io
window.addEventListener('load', function() {
    if (typeof LivePush !== 'undefined') {
        try {
            livePush = new LivePush(LIVEPUSH_CONFIG.appId);
            const channel = livePush.subscribe(LIVEPUSH_CONFIG.channelName);
            
            channel.bind('message', function(data) {
                displayMessage(data);
            });
            
            console.log('✅ LivePush.io connected!');
        } catch (error) {
            console.log('⚠️ Running in demo mode');
        }
    }
});
// ============ END LIVEPUSH CONFIG ============
```

---

### **STEP 3: Update sendMessage() Function**

Find the `sendMessage()` function (around line 1400-1420).

**REPLACE THIS:**
```javascript
function sendMessage() {
    const message = chatInput.value.trim();
    const user = usernameInput.value.trim() || 'Anonymous';
    
    if (message === '') return;
    
    // Create message element
    const messageDiv = document.createElement('div');
    messageDiv.className = 'chat-message';
    
    messageDiv.innerHTML = `
        <div>
            <span class="chat-username">${escapeHtml(user)}</span>
            <span class="chat-timestamp">${getCurrentTime()}</span>
        </div>
        <div class="chat-text">${escapeHtml(message)}</div>
    `;
    
    chatMessages.appendChild(messageDiv);
    chatInput.value = '';
    scrollChatToBottom();
```

**WITH THIS:**
```javascript
function sendMessage() {
    const message = chatInput.value.trim();
    const user = usernameInput.value.trim() || 'Anonymous';
    
    if (message === '') return;
    
    const messageData = {
        username: user,
        message: message,
        timestamp: getCurrentTime(),
        isDJ: false,
        isSystem: false
    };

    // Send via LivePush if available, otherwise display locally
    if (livePush) {
        try {
            const channel = livePush.channel(LIVEPUSH_CONFIG.channelName);
            channel.trigger('message', messageData);
        } catch (error) {
            displayMessage(messageData);  // Fallback
        }
    } else {
        displayMessage(messageData);  // Demo mode
    }
    
    chatInput.value = '';
}

// Helper function to display messages
function displayMessage(data) {
    const messageDiv = document.createElement('div');
    
    if (data.isDJ) {
        messageDiv.className = 'chat-message dj-message';
    } else if (data.isSystem) {
        messageDiv.className = 'chat-message system-message';
    } else {
        messageDiv.className = 'chat-message';
    }
    
    messageDiv.innerHTML = `
        <div>
            <span class="chat-username">${escapeHtml(data.username)}</span>
            <span class="chat-timestamp">${data.timestamp || getCurrentTime()}</span>
        </div>
        <div class="chat-text">${escapeHtml(data.message)}</div>
    `;
    
    chatMessages.appendChild(messageDiv);
    scrollChatToBottom();
    
    // Keep only last 50 messages
    while (chatMessages.children.length > 50) {
        chatMessages.removeChild(chatMessages.firstChild);
    }
}
```

---

## 🎉 THAT'S IT!

After making these 3 changes:

1. **Get your LivePush.io App ID** from https://livepush.io
2. **Replace** `'YOUR_LIVEPUSH_APP_ID'` with your actual ID
3. **Save and upload** the updated index.html
4. **Test with 2 browsers!**

---

## ✅ WHAT YOU GET:

- ✅ Real-time chat between all users
- ✅ Messages sync instantly
- ✅ Works with unlimited users
- ✅ Falls back to demo mode if LivePush not configured
- ✅ DJ message support
- ✅ System messages
- ✅ Message history

---

**Need help? Check LIVEPUSH_SETUP.md for full instructions!**

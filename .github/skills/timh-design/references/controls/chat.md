# Chat Interface
Below is an example chat interface:

```css
.chat
{
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 440px;
    height: 640px;
    background-color: var(--color-light);
    border: solid var(--border-width) var(--color-separator);
    border-radius: var(--radius);
    overflow: hidden;
    transition: border-color var(--transition-standard);
}

.chat:hover
{
    border-color: var(--color-accent);
}

/* Header */
.chat__header
{
    text-align: left;
    padding: var(--space-medium);
    border-bottom: solid var(--border-width) var(--color-separator);
}

.chat__header h1
{
    font-family: "timh-title";
    font-size: var(--text-lg);
}

.chat__header p
{
    font-size: var(--text-sm);
    color: var(--color-muted);
    margin-top: var(--space-small);
}

/* Messages */
.chat__messages
{
    flex: 1;
    overflow-y: auto;
    padding: var(--space-medium);
    display: flex;
    flex-direction: column;
    gap: var(--space-medium);
}

.chat__msg
{
    display: flex;
    flex-direction: column;
    max-width: 80%;
}

.chat__msg--user
{
    align-self: flex-end;
    align-items: flex-end;
}

.chat__msg--bot
{
    align-self: flex-start;
    align-items: flex-start;
}

.chat__meta
{
    font-size: var(--text-sm);
    color: var(--color-muted);
    margin-bottom: var(--space-small);
}

.chat__bubble
{
    padding: var(--space-small) var(--space-medium);
    border-radius: var(--radius);
    border: solid var(--border-width) var(--color-separator);
    background-color: var(--color-light);
    font-size: var(--text-md);
    transition: border-color var(--transition-standard);
}

.chat__bubble:hover
{
    border-color: var(--color-accent);
}

.chat__msg--user .chat__bubble
{
    background-color: var(--color-accent);
    color: var(--color-light);
    border-color: var(--color-accent);
}

/* Typing indicator */
.chat__typing
{
    display: flex;
    gap: 6px;
    align-items: center;
    padding: var(--space-small) var(--space-medium);
}

.chat__typing span
{
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: var(--color-muted);
    animation: chat-blink 1.4s infinite both;
}

.chat__typing span:nth-child(2) { animation-delay: 0.2s; }
.chat__typing span:nth-child(3) { animation-delay: 0.4s; }

@keyframes chat-blink
{
    0%, 80%, 100% { opacity: 0.2; }
    40% { opacity: 1; }
}

/* Composer */
.chat__composer
{
    display: flex;
    gap: var(--space-small);
    align-items: flex-end;
    padding: var(--space-medium);
    border-top: solid var(--border-width) var(--color-separator);
}

.chat__input
{
    flex: 1;
    padding: var(--space-small);
    border: solid var(--border-width) var(--color-muted);
    border-radius: var(--radius);
    background-color: var(--color-light);
    font-family: "timh-text";
    font-size: var(--text-md);
    resize: none;
    max-height: 120px;
    transition: border-color var(--transition-standard);
}

.chat__input:focus
{
    outline: none;
    border-color: var(--color-accent);
}

.chat__send
{
    padding: var(--space-small) var(--space-medium);
    border-radius: var(--radius);
    border: solid var(--border-width) var(--color-dark);
    color: var(--color-dark);
    background-color: var(--color-light);
    font-family: "timh-text";
    font-size: var(--text-md);
    cursor: pointer;
    transition: background-color var(--transition-standard), color var(--transition-standard), border-color var(--transition-standard);
}

.chat__send:hover
{
    background-color: var(--color-accent);
    color: var(--color-light);
    border-color: var(--color-accent);
}
```

And the HTML:

```html
<div class="chat">
    <div class="chat__header">
        <h1>TIMH Assistant</h1>
        <p>Always here to help</p>
    </div>

    <div class="chat__messages" id="chatMessages">
        <div class="chat__msg chat__msg--bot">
            <div class="chat__meta">Assistant</div>
            <div class="chat__bubble">Hi there! I'm your assistant. How can I help you today?</div>
        </div>
        <div class="chat__msg chat__msg--user">
            <div class="chat__meta">You</div>
            <div class="chat__bubble">Can you tell me a bit about what you can do?</div>
        </div>
        <div class="chat__msg chat__msg--bot">
            <div class="chat__meta">Assistant</div>
            <div class="chat__bubble">Of course! I can answer questions, draft text, summarize documents, and more. Just type below to get started.</div>
        </div>
    </div>

    <div class="chat__composer">
        <textarea class="chat__input" id="chatInput" rows="1" placeholder="Type a message..."></textarea>
        <button class="chat__send" id="chatSend">Send</button>
    </div>
</div>
```
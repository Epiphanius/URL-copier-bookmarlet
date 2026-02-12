# URL-copier-bookmarlet
On klick to the bookmarklet-link the script shall copy the URL of the visited website to the clipboard, after it has removed the junk of tracking keys.
Logic: It parses the URL and iterates through a "junk" list to delete specific tracking keys.
Cleaner UI: Instead of a standard browser alert() (which you have to click to close), this creates a small, dark notification in the top-right corner that disappears automatically after 2 seconds.
Reliability: It handles the URL structure more safely than simple regex, ensuring you don't accidentally break the link.

## How to Install it in Firefox
Open Firefox and ensure your Bookmarks Toolbar is visible (Ctrl + Shift + B if it’s hidden).
Right-click on any empty space on the Bookmarks Toolbar and select Add Bookmark.
Name: Give it a name like Copy URL.
URL: Paste the entire block of code from below into the "URL" or "Location" field.
Save: Click "Save" or "Add".

## How it Works
Navigate to any website you want to share.
Click the "Copy URL" bookmark on your toolbar.
The script captures window.location.href and pushes it to your system clipboard.
A small alert will confirm it's done (you can remove the alert() part of the code if you want it to be silent).

javascript:(function() {
try {
const url = new URL(window.location.href);
const params = url.searchParams;
const junk = ['utm_source', 'utm_medium', 'utm_campaign', 'utm_term', 'utm_content', 'fbclid', 'ref', 'gclid'];
junk.forEach(key => params.delete(key));
const cleanURL = url.toString();
navigator.clipboard.writeText(cleanURL).then(() => {
console.log('Cleaned URL copied: ' + cleanURL);
/* Optional: Visual feedback */
const el = document.createElement('div');
el.textContent = 'Clean URL Copied!';
Object.assign(el.style, {
position: 'fixed', top: '10px', right: '10px', padding: '10px',
background: '#333', color: '#fff', zIndex: '9999', borderRadius: '5px'
});
document.body.appendChild(el);
setTimeout(() => el.remove(), 2000);
});
} catch (e) {
alert('Error cleaning URL');
}
})();

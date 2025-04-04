<h1>Unicode XSS Walkthorugh</h1>
<a href="main.html">Go back to Walkthroughs Page</a>
<hr>

<p>This is my first attempt at a moderate lab and I anticipate that it will take a lot more research and patience than the easy labs. The moderate labs are worth 5 points a pop and this first lab is called Unicode XSS.</p>
    
<h2>Initial Input Test</h2>
<p>As with all starts to an XSS challenge, we start with the input of 'User447' to see if we can observe how the application handles our input. In this case, the input is reflected both on the page and in the URL.</p>
<img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/unicodeXSS/image1.png" alt="Input Image 1">
<img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/unicodeXSS/image2.png" alt="Input Image 2">
    
<h2>Injecting a Simple XSS Payload</h2>
<p>The next step is to inject a simple XSS payload into the input field to see how the lab reacts to script tags and similar elements.</p>
    
<pre><code>&lt;script&gt;alert(1)&lt;/script&gt;</code></pre>
    
<img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/unicodeXSS/image3.png" alt="Input Image 3">
    
<p>The output in the page source shows that the <code>&lt;</code> and <code>&gt;</code> tags are being sanitised by the application. However, everything else seems to be going through fine. If we can find a way to bypass this, we should have a working script.</p>
    
<img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/unicodeXSS/image4.png" alt="Input Image 4">
    
<h2>Understanding Unicode's Role</h2>
<p>The title of the lab is Unicode, suggesting that a Unicode-based payload might be required. However, Unicode XSS payloads are less commonly discussed, so research is necessary.</p>
    
<p>Unicode is a universal character encoding standard that provides a unique number for every character, regardless of platform, program, or language. It supports a vast range of characters from different writing systems, symbols, and emojis.</p>
    
<h3>Key Aspects of Unicode:</h3>
<ul>
<li>Uses code points (e.g., U+0041 for 'A').</li>
<li>Supports multiple encoding formats, including UTF-8, UTF-16, and UTF-32.</li>
<li>Covers over 149,000 characters across multiple scripts.</li>
<li>Ensures consistent text representation across systems.</li>
</ul>
    
<h2>Finding a Unicode-Based Bypass</h2>
<p> Now that Unicode has been defined and its behaviour explained, the next step is to explore how it can be implemented in a payload to bypass input sanitisation mechanisms. After extensive research and with assistance from various sources, a useful reference was found:(<a href="https://www.securitum.com/unicodes_role_in_xss_vulnerabilities">source</a>)</p>
    
<p>In this post, Jacek Siwek highlights that certain Unicode characters may bypass validation mechanisms, potentially leading to successful XSS attacks. He further explains that some databases exhibit behaviour where specific Unicode characters are automatically converted into their ASCII equivalents during storage. This transformation can reintroduce malicious payloads that were previously filtered, thereby exposing the application to XSS even when sanitisation appears to be in place.</p>
    
<h3>Unicode Character Examples:</h3>
<ul>
<li><code>&lt;</code> is the less-than sign (U+003C)</li>
<li><code>﹤</code> is the small less-than sign (U+FE64)</li>
<li><code>＜</code> is the fullwidth less-than sign (U+FF1C)</li>
</ul>
    
<p>Here are three Unicode characters that appear visually similar but have different Unicode code points. The theory is that while a database may filter standard < and > characters (i.e., less-than and greater-than), using the fullwidth versions ＜ (U+FF1C) and ＞ (U+FF1E) may bypass validation. The sanitisation routine may not recognise these as dangerous, mistakenly treating them as harmless text rather than potential HTML tags, thereby enabling injection of malicious code.</p>

<h2>Finding a Working Exploit</h2>
<p>With the discovery of the fullwidth and small-width less-than characters, the original payload can be tweaked to try and pop the alert. Putting the standard and modified payloads side by side shows how they differ. Once again the idea is that the sanitisation doesn’t catch on to what these characters actually do, and lets them through, thinking they’re harmless. If that happens, the payload slips past the sanitisation and the alert will pop!</p>

<pre><code>＜script＞alert(document.cookie)＜/script＞ // Fullwidth Payload
&lt;script&gt;alert(doscument.cookie)&lt;/script&gt; // Normal Payload
﹤script﹥alert(document.cookie)﹤/script﹥ // Small-width Payload</code></pre>

<h2>Trying the Fullwidth Payload</h2>

<p>As shown in the following screenshots, the fullwidth payload successfully tricked the web app into triggering an XSS alert. This led to getting the flag and completing the lab. Interestingly, checking the page source shows that the web app converted the Unicode character ＜ into its ASCII equivalent &lt;, without recognising it was part of a malicious script. Futher reinforcing the source from Jacek Siwek.</p>

<img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/unicodeXSS/image5.png" alt="Input Image 5">
<img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/unicodeXSS/image6.png" alt="Input Image 6">

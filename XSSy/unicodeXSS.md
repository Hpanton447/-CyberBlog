    <title>Unicode XSS</title>
    
    <h1>Unicode XSS</h1>
    <p>This is my first attempt at a moderate lab and I anticipate that it will take a lot more research and patience than the easy labs. The moderate labs are worth 5 points a pop and this first lab is called Unicode XSS.</p>
    
    <h2>Initial Input Test</h2>
    <p>As with all starts to an XSS challenge, we start with the input of 'User447' to see if we can observe how the application handles our input. In this case, the input is reflected both on the page and in the URL.</p>
    <img src="image1.png" alt="Input Image 1">
    <img src="image2.png" alt="Input Image 2">
    
    <h2>Injecting a Simple XSS Payload</h2>
    <p>The next step is to inject a simple XSS payload into the input field to see how the lab reacts to script tags and similar elements.</p>
    
    <pre><code>&lt;script&gt;alert(1)&lt;/script&gt;</code></pre>
    
    <img src="image3.png" alt="Input Image 3">
    
    <p>The output in the page source shows that the <code>&lt;</code> and <code>&gt;</code> tags are being sanitised by the application. However, everything else seems to be going through fine. If we can find a way to bypass this, we should have a working script.</p>
    
    <img src="image4.png" alt="Input Image 4">
    
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
    <p>After extensive research, a post by Jacek Siwek (<a href="https://www.securitum.com/unicodes_role_in_xss_vulnerabilitiesn">source</a>) discusses how Unicode can be used to bypass validation mechanisms, potentially leading to XSS vulnerabilities.</p>
    
    <p>Some databases automatically convert certain Unicode characters into their ASCII equivalents during data storage, which could inadvertently bypass XSS protections.</p>
    
    <h3>Unicode Character Examples:</h3>
    <ul>
        <li><code>&lt;</code> is the less-than sign (U+003C)</li>
        <li><code>﹤</code> is the small less-than sign (U+FE64)</li>
        <li><code>＜</code> is the fullwidth less-than sign (U+FF1C)</li>
    </ul>
    
    <p>Although the database filters out standard <code>&lt;</code> and <code>&gt;</code> tags, using fullwidth versions might bypass validation as they are not recognised as harmful HTML but could still function as part of a malicious script.</p>

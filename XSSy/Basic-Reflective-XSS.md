<h1> This is the Basic Reflective XSS Walkthorugh </h1>
<hr>

<p>This is the first XSS challenge on XSSy, and as such, it is designed to be the simplest one. It introduces the fundamental concept of XSS, demonstrating what an ideal outcome should look like. Below is a basic page with an input field asking for your name.</p>

<div style="text-align: left;">
  <img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/89fc110165cc5825a0d3cca5094faf75f12f22f9/XSSy/images/basicReflectiveXSS/image1.png" alt="XSSY Logo" width="300" height="150">
</div>

<p> A quick input of 'User447' reveals that the value entered is reflected not only on the page but also in the URL. Since we now know the input is being reflected on the page, we can proceed to craft a basic payload to try and trigger an alert.</p>
  
 <div style="text-align: left;">
  <img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/basicReflectiveXSS/image2.png" alt="XSSY Logo" width="450" height="150">
</div> 
  
<p> XSS works by injecting malicious code (typically JavaScript) into a website or web application. There are various methods to achieve this, as will be demonstrated throughout these guides, but the simplest approach involves using the &lt;script&gt; tags. Below is an example of a basic XSS payload.</p>

<pre><code>// This is a simple XSS payload 
&lt;script&gt;alert(1)&lt;/script&gt;;</code></pre>

<p>The code &lt;script&gt;alert(1)&lt;/script&gt; is a simple example of a Cross-Site Scripting (XSS) payload. Here’s a break down of what each part does:</p>

<ul>
  <li>&lt;script&gt;: This tag is used in HTML to define a block of JavaScript code.</li>
  <li>alert(1): This is a JavaScript function that triggers a browser alert box displaying the number 1.</li>
  <li>&lt;/script&gt;: This closes the <script> tag, marking the end of the JavaScript code.</li>
</ul>

<p>When this code is injected into a vulnerable website or application, it will execute the JavaScript, causing a pop-up alert with the number 1 to appear in the user's browser. This demonstrates a basic XSS attack, where malicious JavaScript is injected into a web page that is then executed in the context of the user's browser. Below we can see this on the website:</p>


 <div style="text-align: left;">
  <img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/refs/heads/main/XSSy/images/basicReflectiveXSS/image3.png" alt="XSSY Logo" width="800" height="600">
</div> 

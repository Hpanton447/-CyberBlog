<h1> This is the Basic Reflective XSS Walkthorugh </h1>
<hr>

<p>This is the first XSS challenge presented on xssy, and as such it should be the most easy of them all! This challenge shows the basic concept of XSS and shows what an ideal outcome would look like. Below is challenge a basic page with an input askign for our name</p>

<div style="text-align: left;">
  <img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/89fc110165cc5825a0d3cca5094faf75f12f22f9/XSSy/images/basicReflectiveXSS/image1.png" alt="XSSY Logo" width="300" height="150">
</div>

<p> A quick input of 'User447' shows the value we put in is reflected not only on the page but also in the url aswell. Know we now that the input is reflected onto the page we can try building a basic payload to trigger an alert. </p>
  
 <div style="text-align: left;">
  <img src="https://raw.githubusercontent.com/Hpanton447/CyberBlog/89fc110165cc5825a0d3cca5094faf75f12f22f9/XSSy/images/basicReflectiveXSS/image2.png" alt="XSSY Logo" width="300" height="150">
</div> 
  
<p> XSS works by injecting malicious code (usually JavaScript) into a website or web application. This can be done in a manor of differnt ways as will be shown throught these guides but the most simple way is using the &lt;script&gt; tags. Below is an example of a simple XSS payload. </p>

<pre><code>//This is a simple XSS payload <script>alert(1)</script>;</code></pre>

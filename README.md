<h2>microbitcoin</h2>



<p>Micro webshop accepting payments in bitcoin and other payment options.
I developped <a href="http://microbitcoin.net">microbitcoin.net</a> in RoR (Rails 3) starting from Dave Thomas awesome tutorial &quot;Agile Web Development in Rails&quot;. It shows a bitcoin cart/checkout (allowing other payment methods) with email notification, bitcoin uri qrcode, pdf invoice download etc.. A new bitcoin address is generated for each transaction. The app comes with full admin capability to create and update a product catalog. I integrated a deterministic bitcoin wallet so that the shopkeeper can use a regular electrum wallet to watch payments while the web server is not holding any private key. The seed of the electrum wallet can be safely kept offline.The app knows only the master public key of the wallet to generate bitcoin addresses: this is the safest option for a webshop accepting bitcoin payments.</p>

<h4>Who should use microbitcoin?</h4>

<p>Small webshop selling physical goods (sales of digital goods are not yet supported: see TO DO), blogger, event organizer,etc.</p>

<h4>Main features:</h4>

<ul>
<li>Product catalog with full admin capabilities: create products with pictures, update prices, etc.. 
Prices are set in bitcoin and shippig costs are set in fiat currency (e.g. euros). Amounts are displayed both in fiat currency and bitcoins.<br></li>
<li>Two-step check out: shipping details form, invoice. No sign up is required.<br></li>
<li>Bitcoin invoice: a new bitcoin address is generated for each invoice, using an electrum wallet master public key. This feature uses Pavol Rusnak&#39;s &#39;bitcoin-addrgen&#39; gem.</li>
<li>PDF invoice: a pdf invoice is generated and can be downloaded by the customer at the time of order. If payment in bitcoin was selected, the pdf includes the bitcoin uri qrcode.</li>
<li>email notifications upon order and payment received (using blockchain.info API).</li>
<li>Photo gallery carousel</li>
<li>Javascript cart in side bar</li>
<li>Sidebar navigation with custom css (no bootstrap).</li>
<li>Static pages: FAQ, Shipping conditions, etc</li>
<li>Locale switch (flags)</li>
<li>No third party service is called except blockchain.info for payment receive notifications and bitcoincharts for current exchange rate. Default rate can be set in config file.</li>
</ul>

<h4>Usage</h4>

<ol>
<li><p>Download and install your electrum wallet application from electrum.org
Install Rails 3 (upgrade to Rails 4 is on the TO DO list)
Install postgreSQL database</p></li>
<li><p>$ git clone <a href="https://github.com/pierrenoizat/webshop.git">https://github.com/pierrenoizat/webshop.git</a></p></li>
<li><p>$ bundle install</p></li>
<li><p>Edit config/application.rb file to enter your own electrum wallet master public key (export master public key from your electrum wallet) as $MPK global variable.</p></li>
<li><p>Edit user.rb to change &quot;wibble&quot; by any random string of your choice in
Digest::SHA2.hexdigest(password + &quot;wibble&quot; + salt)</p></li>
<li><p>Edit config/environments/development.rb and production.rb to enter your own gmail password.</p></li>
<li><p>Comment out the following line if you want to have emails delivered in development:
config.action<em>mailer.perform</em>deliveries = false</p></li>
<li><p>Edit db/seeds.rb to enter your user name and password for the postgreSQL database in
user = User.create(:name =&gt; &quot;Pierre&quot;, :password =&gt; &quot;password&quot;, :password_confirmation =&gt; &quot;password&quot;)</p></li>
<li><p>$ rake db:setup</p></li>
<li><p>$ rails server</p></li>
<li><p>Visit http://localhost:3000, start browsing the catalog and shopping..
Fork the code to go after the TO DO features.</p></li>
</ol>

<h4>TO DO:</h4>

<ul>
<li>pretty css with bootstrap</li>
<li>add instant payment receive notification to sell digital goods (download links).</li>
<li>develop test</li>
<li>make javascript work with IE. Some visual effects are not displayed properly with IE while they work fine with real web browsers like Firefox, Chrome or Safari.</li>
<li>add quantity increment/decrement to cart functionnality. Right now only &quot;add one to cart&quot; and &quot;empty cart&quot; buttons are present.</li>
<li>add bank card payment options. Right now only bitcoins and checks appear in the payment option list.</li>
<li>display VAT amount in invoices</li>
<li>develop an audit server that will periodically visit the shop to generate a bitcoin address: the audit server can then check that the address belongs to the wallet and send an alert if there is a mismatch. The audit server needs only the master public key of the wallet. The audit server makes it harder to tamper with the payment addresses: both the audit server and the webshop app server must be compromised simultaneously to tamper with the master public key, Right now, the security check can be performed manually by the shop keeper or by the shopper using bitcoinrad.io (another web app I developped as a security feature: see <a href="http://www.bitcoinrad.io">bitcoinrad.io</a> website).</li>
<li>Update to Rails 4</li>
</ul>

<h5>More on preventing man-in-the-middle attacks</h5>

<p>Publish the master public key on several social networks and key servers: this will allow your customers to check that the address belongs to you before paying your invoice (see bitcoinrad.io for details). This is not a requirement but its a sure and simple way to mitigate the risk of a man-in-the-middle attack on your bitcoin payment addresses. Knowing your master public key will allow also the taxman and your competitors to track your bitcoin revenues but this is the price to pay for ultimate security. Bear in mind that your bitcoin sales are probably only a fraction of your sales since you offer several payment options. If you are not comfortable with this level of transparency, then the audit server (see TO DO list) keeps your bitcoin sales figures private while achieving ultimate security at the cost of an additionnal server.</p>

<h4>Thanks and Credits</h4>

<p>Matej Danter</p>

<p>David Heinemeier Hansson</p>

<p>Sam Ruby</p>

<p>Pavol Rusnak</p>

<p>Chris Savery</p>

<p>Dave Thomas</p>

<p>Donations welcome to 1GzN629RXup74eT1LsddKgnKvMtkS1ULHp. Donations help me cover the costs of hosting microbitcoin.net.</p>

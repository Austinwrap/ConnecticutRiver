<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Connecticut Riverline - Adventure PDF Guides</title>
    <style>
        /* Reset and Base Styles */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Segoe UI', Arial, sans-serif; line-height: 1.6; background-color: #e8ecef; color: #2d3436; overflow-x: hidden; }

        /* Header */
        header {
            background: url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80') no-repeat center center/cover;
            height: 100vh;
            color: white;
            text-align: center;
            padding: 20px;
            padding-top: 150px;
            text-shadow: 3px 3px 8px rgba(0, 0, 0, 0.9);
            border-bottom: 6px solid #3498db;
            position: relative;
            overflow: hidden;
        }
        header::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.2); /* Lightened overlay */
            z-index: 1;
        }
        header h1, header p, header .cta-btn, header .enter-btn, header .scroll-prompt { position: relative; z-index: 2; }
        header h1 { font-size: 2.8em; margin-bottom: 15px; letter-spacing: 2px; animation: slideIn 1s ease-out; }
        header p { font-size: 1.2em; font-weight: 300; margin-bottom: 20px; animation: fadeIn 1.5s ease-out; }
        .cta-btn, .enter-btn {
            display: inline-block;
            padding: 12px 30px;
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
            text-decoration: none;
            border-radius: 50px;
            font-size: 1.2em;
            border: 2px solid #2980b9;
            transition: all 0.4s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            margin: 10px auto;
            cursor: pointer;
        }
        .cta-btn:hover, .enter-btn:hover { background: linear-gradient(45deg, #2980b9, #1b5e91); transform: scale(1.1); box-shadow: 0 8px 20px rgba(0,0,0,0.4); }
        .enter-btn { background: linear-gradient(45deg, #e67e22, #d35400); border-color: #d35400; }
        .scroll-prompt {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 1em;
            color: #fff;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.7);
            animation: bounce 2s infinite;
        }

        /* PDF Form Popup */
        #pdf-form-container, .activity-popup {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 3;
            justify-content: center;
            align-items: center;
        }
        #pdf-form, .activity-details {
            background: #fff;
            padding: 20px;
            border-radius: 10px;
            max-width: 90%;
            width: 400px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            text-align: left;
            position: relative;
        }
        #pdf-form h3, .activity-details h3 { color: #2c3e50; margin-bottom: 15px; }
        #pdf-form label { display: block; margin: 10px 0 5px; font-weight: 600; }
        #pdf-form input, #pdf-form select { width: 100%; padding: 10px; margin-bottom: 15px; border: 1px solid #dfe6e9; border-radius: 6px; }
        #pdf-form button { padding: 10px; background: linear-gradient(45deg, #3498db, #2980b9); color: white; border: none; border-radius: 6px; width: 100%; cursor: pointer; }
        #pdf-form button:hover { background: linear-gradient(45deg, #2980b9, #1b5e91); }
        #close-pdf-form, .close-activity {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 1.5em;
            color: #2c3e50;
            cursor: pointer;
            border: none;
            background: none;
            padding: 0;
            width: 24px;
            height: 24px;
            line-height: 24px;
            text-align: center;
        }
        #close-pdf-form:hover, .close-activity:hover { color: #e74c3c; }
        .activity-details ul { list-style: disc; padding-left: 20px; }
        .activity-details li { margin: 5px 0; }

        /* Animations */
        @keyframes slideIn { from { transform: translateY(-50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes bounce { 0%, 20%, 50%, 80%, 100% { transform: translateY(0); } 40% { transform: translateY(-10px); } 60% { transform: translateY(-5px); } }

        /* Sections */
        section { padding: 40px 15px; text-align: center; }
        .about, .pricing, .quote { background-color: #fff; margin: 20px auto; max-width: 100%; width: 100%; border-radius: 10px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); border: 1px solid #dfe6e9; padding: 30px; transition: transform 0.3s ease; }
        .about:hover, .pricing:hover, .quote:hover { transform: translateY(-3px); }
        h2 { color: #2c3e50; font-size: 2em; margin-bottom: 20px; border-bottom: 3px solid #3498db; display: inline-block; padding-bottom: 5px; }
        p { font-size: 1em; }

        /* Destinations */
        .destinations { display: flex; flex-direction: column; align-items: center; gap: 20px; }
        .destination { width: 100%; max-width: 380px; background: #f7f9fb; padding: 20px; border-radius: 10px; border: 1px solid #dfe6e9; transition: all 0.3s ease; }
        .destination:hover { transform: scale(1.02); box-shadow: 0 6px 20px rgba(0,0,0,0.15); }
        .destination h3 { color: #2980b9; font-size: 1.4em; margin-bottom: 10px; cursor: pointer; }
        .destination h3:hover { color: #1b5e91; text-decoration: underline; }

        /* Pricing Table */
        .pricing-table { width: 100%; margin: 20px auto; border-collapse: separate; border-spacing: 0; border: 1px solid #dfe6e9; border-radius: 10px; overflow: hidden; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
        .pricing-table th, .pricing-table td { padding: 15px; text-align: left; border-bottom: 1px solid #dfe6e9; font-size: 0.95em; }
        .pricing-table th { background: linear-gradient(45deg, #2c3e50, #34495e); color: white; font-size: 1em; }
        .pricing-table tr:last-child td { border-bottom: none; }
        .pricing-table tr:nth-child(even) { background-color: #f9fbfc; }

        /* Quote Generator */
        .quote-generator { max-width: 100%; margin: 20px auto; text-align: left; background: #f7f9fb; padding: 20px; border-radius: 10px; border: 1px solid #dfe6e9; box-shadow: 0 4px 15px rgba(0,0,0,0.05); }
        .quote-generator label { display: block; margin: 10px 0 5px; font-weight: 600; color: #2c3e50; font-size: 1em; }
        .quote-generator input, .quote-generator select { width: 100%; padding: 10px; margin-bottom: 15px; border: 1px solid #dfe6e9; border-radius: 6px; font-size: 1em; transition: border-color 0.3s ease; }
        .quote-generator input:focus, .quote-generator select:focus { border-color: #3498db; outline: none; }
        .quote-generator button { padding: 10px 20px; background: linear-gradient(45deg, #e67e22, #d35400); color: white; border: none; border-radius: 6px; cursor: pointer; font-size: 1em; transition: all 0.3s ease; width: 100%; }
        .quote-generator button:hover { background: linear-gradient(45deg, #d35400, #b74700); transform: scale(1.03); }
        #quote-result { margin-top: 20px; font-size: 1.1em; color: #27ae60; }

        /* Footer */
        footer { background: linear-gradient(45deg, #2c3e50, #34495e); color: white; text-align: center; padding: 20px; border-top: 6px solid #3498db; }
        footer a { color: #74b9ff; text-decoration: none; font-weight: 500; transition: color 0.3s ease; }
        footer a:hover { color: #a29bfe; text-decoration: underline; }

        /* iPhone Optimization (max-width: 430px) */
        @media (max-width: 430px) {
            header { padding-top: 120px; }
            header h1 { font-size: 2.2em; }
            header p { font-size: 1em; }
            .cta-btn, .enter-btn { font-size: 1em; padding: 10px 25px; width: 80%; max-width: 300px; }
            .scroll-prompt { font-size: 0.9em; bottom: 15px; }
            #pdf-form, .activity-details { width: 90%; padding: 15px; }
            section { padding: 30px 10px; }
            h2 { font-size: 1.8em; }
            .destination { padding: 15px; }
            .pricing-table th, .pricing-table td { padding: 10px; font-size: 0.85em; }
            .quote-generator { padding: 15px; }
            .quote-generator label { font-size: 0.9em; }
            .quote-generator input, .quote-generator select { padding: 8px; }
            .quote-generator button { padding: 8px 15px; }
            #quote-result { font-size: 1em; }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <h1>Connecticut Riverline</h1>
        <p>Unleash Your Adventure with PDF Guides Starting at $29!</p>
        <div class="cta-btn" onclick="showPdfForm()">Get Your PDF Guide ($29+)</div>
        <a href="#about" class="enter-btn">Enter the Adventure</a>
        <div class="scroll-prompt">Scroll to Explore More ↓</div>
    </header>

    <!-- PDF Purchase Form -->
    <div id="pdf-form-container">
        <div id="pdf-form">
            <button id="close-pdf-form" onclick="hidePdfForm()">✖</button>
            <h3>Purchase a PDF Guide</h3>
            <label for="pdf-name">Your Name:</label>
            <input type="text" id="pdf-name" placeholder="John Doe" required>
            
            <label for="pdf-email">Email:</label>
            <input type="email" id="pdf-email" placeholder="you@example.com" required>
            
            <label for="pdf-phone">Phone Number:</label>
            <input type="tel" id="pdf-phone" placeholder="123-456-7890" required>
            
            <label for="pdf-guide">Select PDF Guide:</label>
            <select id="pdf-guide" required>
                <option value="Basic River Guide ($29)">Basic River Guide ($29)</option>
                <option value="Mountain Explorer ($49)">Mountain Explorer ($49)</option>
                <option value="DIY Intense Guide ($79)">DIY Intense Guide ($79)</option>
            </select>
            
            <label for="pdf-payment">Venmo or PayPal Username:</label>
            <input type="text" id="pdf-payment" placeholder="@username" required>
            
            <button onclick="submitPdfForm()">Send Purchase Request</button>
        </div>
    </div>

    <!-- Activity Popups -->
    <div id="ct-river-popup" class="activity-popup">
        <div class="activity-details">
            <button class="close-activity" onclick="hideActivity('ct-river-popup')">✖</button>
            <h3>Connecticut River Overnight</h3>
            <p>1 or 2 nights kayaking and camping ($149/$199 per person, max 8 people):</p>
            <ul>
                <li>Meet at launch site, use our kayaks</li>
                <li>Paddle downriver with guided support</li>
                <li>Set up camp with provided food/drinks</li>
                <li>Explore riverside trails and relax</li>
                <li>Return next day (or day after for 2 nights)</li>
            </ul>
        </div>
    </div>
    <div id="farmington-popup" class="activity-popup">
        <div class="activity-details">
            <button class="close-activity" onclick="hideActivity('farmington-popup')">✖</button>
            <h3>Farmington River Day Trip</h3>
            <p>One-day canoe/kayak adventure ($80 per person):</p>
            <ul>
                <li>Meet at launch site, use our canoes/kayaks</li>
                <li>Guided paddle down the river</li>
                <li>Break for provided lunch</li>
                <li>Navigate rapids or relax on calm waters</li>
                <li>Finish and depart from end point</li>
            </ul>
        </div>
    </div>
    <div id="mountains-popup" class="activity-popup">
        <div class="activity-details">
            <button class="close-activity" onclick="hideActivity('mountains-popup')">✖</button>
            <h3>Mountain Hiking Day</h3>
            <p>Full-day guided hike ($49 per person):</p>
            <ul>
                <li>Meet at base or ride together to mountain</li>
                <li>Tackle ascent with guided support</li>
                <li>Regroup at midpoint for a break</li>
                <li>Summit, snack, and relax at the top</li>
                <li>Descend, regroup, and head home</li>
            </ul>
        </div>
    </div>

    <!-- About Section -->
    <section class="about" id="about">
        <h2>About Us</h2>
        <p>Hey there! I’m your guide to epic adventures along the Connecticut River, Farmington River, and breathtaking mountains across CT, NY, or MA—plus thrilling escapes to Vermont and Maine. My PDF guides bring the excitement to you, packed with everything you need for an unforgettable journey. Ready to dive in?</p>
    </section>

    <!-- Destinations Section -->
    <section>
        <h2>Where the Fun Happens</h2>
        <div class="destinations">
            <div class="destination">
                <h3 onclick="showActivity('ct-river-popup')">Connecticut River</h3>
                <p>Glide along pristine waters, where history meets breathtaking natural splendor.</p>
            </div>
            <div class="destination">
                <h3 onclick="showActivity('farmington-popup')">Farmington River</h3>
                <p>Master exhilarating rapids or enjoy a peaceful paddle—your adventure, your way.</p>
            </div>
            <div class="destination">
                <h3 onclick="showActivity('mountains-popup')">Mountains & More</h3>
                <p>Summit majestic peaks in CT, NY, MA, or venture into the rugged trails of Vermont and Maine.</p>
            </div>
        </div>
    </section>

    <!-- Pricing Section -->
    <section class="pricing">
        <h2>PDF Guide Pricing</h2>
        <p>One-time purchase PDF guides packed with adventure details—click activities above for trip info!</p>
        <table class="pricing-table">
            <tr>
                <th>PDF Guide Type</th>
                <th>Price</th>
                <th>What’s Inside</th>
            </tr>
            <tr>
                <td>Basic River Guide (PDF)</td>
                <td>$29</td>
                <td>Detailed maps, paddling tips, and key stops for Connecticut and Farmington Rivers.</td>
            </tr>
            <tr>
                <td>Mountain Explorer (PDF)</td>
                <td>$49</td>
                <td>Trail guides for CT, NY, MA mountains, gear checklist, and scenic highlights.</td>
            </tr>
            <tr>
                <td>DIY Intense Guide (PDF)</td>
                <td>$79</td>
                <td>Hardcore PDF with everything for solo adventures—gear hacks, route planning, and insider secrets for rivers and peaks.</td>
            </tr>
            <tr>
                <td>Ultimate Adventure (PDF + Group Trip)</td>
                <td>$149–$199/person</td>
                <td>PDF with all rivers and mountains, plus a guided overnight group canoe/hike down the Connecticut River—routes, campsites, survival tips. Use Quote Generator below!</td>
            </tr>
        </table>
    </section>

    <!-- Quote Generator Section for Ultimate Adventure -->
    <section class="quote">
        <h2>Ultimate Adventure Quote Generator</h2>
        <p>Book a group overnight canoe/hike down the Connecticut River (1-8 people). Over 8? We’ll discuss custom pricing via email/phone!</p>
        <div class="quote-generator">
            <label for="name">Your Name:</label>
            <input type="text" id="name" placeholder="John Doe" required>
            
            <label for="phone">Phone Number:</label>
            <input type="tel" id="phone" placeholder="123-456-7890" required>
            
            <label for="email">Email:</label>
            <input type="email" id="email" placeholder="you@example.com" required>
            
            <label for="group-size">Group Size (1-8):</label>
            <input type="number" id="group-size" min="1" max="8" value="1" required>
            
            <label for="nights">Trip Duration:</label>
            <select id="nights" required>
                <option value="149">1 Night ($149/person)</option>
                <option value="199">2 Nights ($199/person)</option>
                <option value="custom">Over 8 People? Custom Quote</option>
            </select>
            
            <label for="trip-date">Select Trip Date:</label>
            <input type="date" id="trip-date" min="2025-03-06" required>
            
            <label for="payment">Venmo or PayPal Username:</label>
            <input type="text" id="payment" placeholder="@username" required>
            
            <button onclick="calculateQuote()">Get Your Quote</button>
            <div id="quote-result"></div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <p>© 2025 Connecticut Riverline. Reach out at <a href="mailto:aytmout@gmail.com">aytmout@gmail.com</a></p>
    </footer>

    <!-- JavaScript for PDF Form, Quote Generator, Activity Popups, and Smooth Scroll -->
    <script>
        // Show PDF Form
        function showPdfForm() {
            document.getElementById('pdf-form-container').style.display = 'flex';
        }

        // Hide PDF Form
        function hidePdfForm() {
            document.getElementById('pdf-form-container').style.display = 'none';
        }

        // Submit PDF Form
        function submitPdfForm() {
            const name = document.getElementById('pdf-name').value;
            const email = document.getElementById('pdf-email').value;
            const phone = document.getElementById('pdf-phone').value;
            const guide = document.getElementById('pdf-guide').value;
            const payment = document.getElementById('pdf-payment').value;

            if (!name || !email || !phone || !guide || !payment) {
                alert("Please fill out all fields!");
                return;
            }

            const emailBody = `PDF Guide Purchase Request\n\nName: ${name}\nEmail: ${email}\nPhone: ${phone}\nGuide Requested: ${guide}\nVenmo/PayPal: ${payment}\n\nPlease send the PDF guide and confirm payment request via Venmo/PayPal. I’ll wait for your email confirmation before you charge me!`;
            window.location.href = `mailto:aytmout@gmail.com?subject=PDF Guide Purchase Request&body=${encodeURIComponent(emailBody)}`;
            hidePdfForm();
        }

        // Show Activity Popup
        function showActivity(id) {
            document.getElementById(id).style.display = 'flex';
        }

        // Hide Activity Popup
        function hideActivity(id) {
            document.getElementById(id).style.display = 'none';
        }

        // Quote Generator for Ultimate Adventure
        function calculateQuote() {
            const name = document.getElementById('name').value;
            const phone = document.getElementById('phone').value;
            const email = document.getElementById('email').value;
            const groupSize = document.getElementById('group-size').value;
            const pricePerPerson = document.getElementById('nights').value;
            const tripDate = document.getElementById('trip-date').value;
            const payment = document.getElementById('payment').value;

            if (!name || !phone || !email || !groupSize || !tripDate || !payment) {
                document.getElementById('quote-result').innerHTML = "Please fill out all fields!";
                return;
            }

            if (pricePerPerson === "custom") {
                const emailBody = `Custom Quote Request for Ultimate Adventure\n\nName: ${name}\nPhone: ${phone}\nEmail: ${email}\nGroup Size: ${groupSize} (Over 8)\nTrip Date: ${tripDate}\nVenmo/PayPal: ${payment}\n\nPlease contact me to discuss pricing and details for a group over 8 people!`;
                document.getElementById('quote-result').innerHTML = `Group over 8? <a href="mailto:aytmout@gmail.com?subject=Ultimate Adventure Custom Quote Request&body=${encodeURIComponent(emailBody)}">Email us to discuss!</a>`;
            } else {
                const total = groupSize * pricePerPerson;
                const nightsText = pricePerPerson == 149 ? "1 Night" : "2 Nights";
                const emailBody = `Booking Request for Ultimate Adventure Group Trip\n\nName: ${name}\nPhone: ${phone}\nEmail: ${email}\nPackage: Ultimate Adventure (Overnight Canoe/Hike)\nGroup Size: ${groupSize}\nDuration: ${nightsText}\nTotal Cost: $${total}\nTrip Date: ${tripDate}\nVenmo/PayPal: ${payment}\n\nPlease confirm availability and send payment request via Venmo/PayPal. We’ll email you back with confirmation before charging!`;
                document.getElementById('quote-result').innerHTML = `Total for ${groupSize} people (${nightsText}): $${total}. <a href="mailto:aytmout@gmail.com?subject=Ultimate Adventure Booking Request&body=${encodeURIComponent(emailBody)}">Email us to book!</a>`;
            }
        }

        // Smooth scroll for "Enter" button
        document.querySelector('.enter-btn').addEventListener('click', function(e) {
            e.preventDefault();
            document.querySelector('#about').scrollIntoView({ behavior: 'smooth' });
        });
    </script>
</body>
</html>

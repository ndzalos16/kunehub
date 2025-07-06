<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Brand - Modern E-commerce</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts - Inter for clean typography -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* Custom CSS for Inter font and smooth scrolling */
        body {
            font-family: 'Inter', sans-serif;
            scroll-behavior: smooth;
        }
        /* Custom hover effect for buttons */
        .btn-primary {
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .btn-primary:hover {
            transform: scale(1.02) translateY(-2px); /* Enhanced hover: slight scale and lift */
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2); /* More pronounced shadow */
        }
        /* Custom hover effect for product cards */
        .product-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
        }
        .product-card:hover {
            transform: scale(1.01) translateY(-5px); /* Enhanced hover: slight scale and lift */
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15); /* More pronounced shadow */
        }
        /* Custom aspect ratio for product images */
        .aspect-ratio-9-16 {
            padding-top: calc(16 / 9 * 100%); /* Height / Width * 100% */
        }

        /* Modern Glassmorphism Navbar */
        .sticky-header {
            background-color: rgba(255, 255, 255, 0.7); /* Semi-transparent white */
            backdrop-filter: blur(8px); /* Frosted glass effect */
            -webkit-backdrop-filter: blur(8px); /* Safari support */
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.03); /* Subtle shadow */
        }
        .sticky-header.scrolled {
            background-color: rgba(255, 255, 255, 0.9); /* More opaque when scrolled */
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1); /* More pronounced shadow when scrolled */
        }

        /* Hamburger menu icon animation */
        .hamburger-icon span {
            display: block;
            width: 25px;
            height: 3px;
            background-color: #333;
            margin: 5px 0;
            transition: all 0.3s ease-in-out;
        }
        .hamburger-icon.open span:nth-child(1) {
            transform: rotate(-45deg) translate(-5px, 6px);
        }
        .hamburger-icon.open span:nth-child(2) {
            opacity: 0;
        }
        .hamburger-icon.open span:nth-child(3) {
            transform: rotate(45deg) translate(-5px, -6px);
        }

        /* --- Animations --- */

        /* General Fade In (can be combined with other transforms) */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .animate-fadeIn { animation: fadeIn 1s ease-out forwards; }

        /* Slide In Up */
        @keyframes slideInUp {
            from { opacity: 0; transform: translateY(50px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-slideInUp { animation: slideInUp 1s ease-out forwards; }

        /* Slide In Left */
        @keyframes slideInLeft {
            from { opacity: 0; transform: translateX(-50px); }
            to { opacity: 1; transform: translateX(0); }
        }
        .animate-slideInLeft { animation: slideInLeft 1s ease-out forwards; }

        /* Slide In Right */
        @keyframes slideInRight {
            from { opacity: 0; transform: translateX(50px); }
            to { opacity: 1; transform: translateX(0); }
        }
        .animate-slideInRight { animation: slideInRight 1s ease-out forwards; }

        /* Pop In (for buttons/CTAs) */
        @keyframes popIn {
            0% { opacity: 0; transform: scale(0.5); }
            80% { opacity: 1; transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        .animate-popIn { animation: popIn 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55) forwards; }

        /* Scale In (for logo, titles) */
        @keyframes scaleIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }
        .animate-scaleIn { animation: scaleIn 0.5s ease-out forwards; }

        /* Bounce for scroll cue arrow */
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }
        .animate-bounce {
            animation: bounce 2s infinite;
        }

        /* Initial hidden state for elements that will animate on scroll */
        [data-animate] {
            opacity: 0;
        }

        /* Specific styling for the hero background text */
        .hero-bg-text {
            font-size: 10vw; /* Responsive font size */
            font-weight: 800;
            color: rgba(255, 255, 255, 0.08); /* Very subtle white */
            pointer-events: none; /* Allows clicks to pass through */
            user-select: none; /* Prevent text selection */
            white-space: nowrap; /* Keep text on one line */
            overflow: hidden; /* Hide overflow if text is too wide */
            text-shadow: 0 0 10px rgba(0,0,0,0.1); /* Subtle shadow for depth */
        }
        @media (min-width: 768px) { /* Adjust for larger screens */
            .hero-bg-text {
                font-size: 8vw;
            }
        }
        @media (min-width: 1024px) { /* Adjust for larger screens */
            .hero-bg-text {
                font-size: 6vw;
            }
        }

        /* Custom blur for the background image */
        .filter-blur-custom {
            filter: blur(3px); /* Reduced blur by 50% from previous 6px */
        }
        /* Parallax background image styling */
        #hero-bg-image {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 80%; /* Adjusted from w-[80%] to CSS for consistency */
            height: 80%; /* Adjusted from h-[80%] to CSS for consistency */
            object-fit: contain;
            transform: translate(-50%, -50%); /* Base centering */
            transition: transform 0.05s linear; /* Smooth movement */
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">

    <!-- Sticky Header -->
    <header id="main-header" class="sticky-header fixed w-full top-0 z-50 py-4 px-6 md:px-12 transition-all duration-300 ease-in-out">
        <nav class="container mx-auto flex justify-between items-center">
            <!-- Logo -->
            <a href="#" class="flex items-center space-x-2 p-2 sm:p-0"> <!-- Added padding for breathing room -->
                <!-- Using the local path provided by the user -->
                <img src="C:\Users\mahom\OneDrive\Documents\javandzalo\92cb7b08-18c6-4032-a1c6-50cea394b8fb-removebg-preview (2).png" alt="Brand Logo" class="h-8 w-8 sm:h-10 sm:w-10 rounded-full shadow-md animate-scaleIn"> <!-- Reduced size on mobile, scaled up on sm+ -->
                <span class="text-2xl font-bold text-indigo-600">YourBrand</span>
            </a>

            <!-- Desktop Navigation -->
            <ul class="hidden md:flex space-x-8 text-lg font-medium">
                <li><a href="#home" class="text-gray-700 hover:text-indigo-600 hover:underline hover:underline-offset-4 transition duration-300 ease-in-out">Home</a></li>
                <li><a href="#products" class="text-gray-700 hover:text-indigo-600 hover:underline hover:underline-offset-4 transition duration-300 ease-in-out">Shop</a></li>
                <li><a href="#about" class="text-gray-700 hover:text-indigo-600 hover:underline hover:underline-offset-4 transition duration-300 ease-in-out">About Us</a></li>
                <li><a href="#contact" class="text-gray-700 hover:text-indigo-600 hover:underline hover:underline-offset-4 transition duration-300 ease-in-out">Contact</a></li>
                <li><a href="#cart" class="text-gray-700 hover:text-indigo-600 hover:underline hover:underline-offset-4 transition duration-300 ease-in-out">Cart (0)</a></li>
            </ul>

            <!-- Mobile Hamburger Menu -->
            <div class="md:hidden">
                <button id="mobile-menu-button" class="focus:outline-none hamburger-icon">
                    <span></span>
                    <span></span>
                    <span></span>
                </button>
            </div>
        </nav>

        <!-- Mobile Menu Overlay -->
        <div id="mobile-menu" class="hidden md:hidden fixed inset-0 bg-white bg-opacity-95 z-40 flex flex-col items-center justify-center space-y-6 text-2xl font-semibold transition-transform transform translate-x-full ease-in-out duration-300">
            <button id="close-menu-button" class="absolute top-6 right-6 text-gray-700 hover:text-indigo-600 text-4xl">&times;</button>
            <a href="#home" class="text-gray-700 hover:text-indigo-600" onclick="toggleMobileMenu()">Home</a>
            <a href="#products" class="text-gray-700 hover:text-indigo-600" onclick="toggleMobileMenu()">Shop</a>
            <a href="#about" class="text-gray-700 hover:text-indigo-600" onclick="toggleMobileMenu()">About Us</a>
            <a href="#contact" class="text-gray-700 hover:text-indigo-600" onclick="toggleMobileMenu()">Contact</a>
            <a href="#cart" class="text-gray-700 hover:text-indigo-600" onclick="toggleMobileMenu()">Cart (0)</a>
        </div>
    </header>

    <main>
        <!-- Hero Section -->
        <section id="home" class="relative bg-gradient-to-br from-indigo-700 via-purple-700 to-pink-600 text-white py-24 md:py-36 min-h-screen flex items-center justify-center overflow-hidden">
            <!-- Existing subtle pattern and black overlay -->
            <div class="absolute inset-0 opacity-20" style="background-image: radial-gradient(#ffffff33 1px, transparent 1px), radial-gradient(#ffffff33 1px, transparent 1px); background-size: 20px 20px; background-position: 0 0, 10px 10px;"></div>
            <div class="absolute inset-0 bg-black opacity-40"></div>

            <!-- UPDATED: Background image with adjusted size, blur, and parallax -->
            <div class="absolute inset-0 z-0 overflow-hidden">
                <!-- The image itself is now absolutely positioned and centered via CSS -->
                <img id="hero-bg-image" src="C:\Users\mahom\OneDrive\Documents\javandzalo\8c885650-1ee8-47f8-acaf-fd408727ee7d-removebg-preview.png" alt="Abstract Background" class="filter-blur-custom opacity-30">
            </div>

            <!-- Large Semi-Transparent Background Text -->
            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 hero-bg-text z-0">
                INNOVATE
            </div>
            <div class="absolute top-[60%] left-1/2 -translate-x-1/2 -translate-y-1/2 hero-bg-text z-0" style="animation-delay: 0.1s;">
                FUTURE
            </div>

            <div class="container mx-auto text-center relative z-10 px-4">
                <h1 class="text-4xl md:text-6xl font-extrabold leading-tight mb-6 drop-shadow-lg animate-slideInUp">
                    Discover Innovation. Live Better.
                </h1>
                <p class="text-lg md:text-xl max-w-2xl mx-auto mb-10 opacity-90 animate-slideInUp" style="animation-delay: 0.3s;">
                    Explore our curated collection of cutting-edge products designed to enhance your everyday life.
                </p>
                <a href="#products" class="btn-primary inline-flex items-center justify-center space-x-2 bg-white text-indigo-700 hover:bg-gray-100 px-8 py-4 rounded-full text-lg font-semibold shadow-xl transition-all duration-300 ease-in-out animate-popIn" style="animation-delay: 0.6s;">
                    <!-- Corrected SVG Icon for the button -->
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                        <path fill-rule="evenodd" d="M7.5 6v.75H5.513c-.96 0-1.76.759-1.76 1.712v10.5c0 .953.799 1.712 1.76 1.712h12.974c.96 0 1.76-.759 1.76-1.712V8.462c0-.953-.799-1.712-1.76-1.712H16.5V6a4.5 4.5 0 10-9 0zm1.5.75a3 3 0 106 0V6a3 3 0 10-6 0v.75z" clip-rule="evenodd" />
                    </svg>
                    <span>Shop Our Collection</span>
                </a>
            </div>

            <!-- Scroll Cue Arrow -->
            <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 z-10">
                <a href="#products" aria-label="Scroll down to products">
                    <svg class="w-8 h-8 text-white animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"></path>
                    </svg>
                </a>
            </div>
        </section>

        <!-- Product Showcase Section -->
        <section id="products" class="py-16 md:py-24 bg-white" data-animate="fadeIn">
            <div class="container mx-auto px-6">
                <h2 class="text-3xl md:text-4xl font-bold text-center mb-12 text-gray-900" data-animate="slideInUp">Our Latest Innovations</h2>

                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                    <!-- Product Card 1 -->
                    <div class="product-card bg-gray-50 rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 ease-in-out max-w-xs sm:max-w-none mx-auto" data-animate="slideInUp" data-delay="0s">
                        <div class="relative w-full aspect-ratio-9-16 mb-4"> <!-- Added bottom margin -->
                            <!-- Reduced image size on mobile, added rounded corners and shadow -->
                            <img src="C:\Users\mahom\OneDrive\Documents\javandzalo\2ae28588-6f1f-459c-923c-1548b6ab902a.png" alt="Product Image 1" class="absolute inset-0 w-full h-full object-cover rounded-lg shadow-md sm:w-[90%] sm:mx-auto">
                        </div>
                        <div class="p-6 text-center"> <!-- Centered text content -->
                            <h3 class="text-xl font-semibold mb-2 text-gray-900">Futuristic Gadget</h3>
                            <p class="text-gray-600 text-sm mb-4">Next-gen tech for a smarter life.</p> <!-- Added subtitle -->
                            <div class="flex justify-center items-center">
                                <button class="btn-primary bg-indigo-600 text-white px-5 py-2 rounded-full text-sm font-medium hover:bg-indigo-700">
                                    View Details
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Product Card 2 -->
                    <div class="product-card bg-gray-50 rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 ease-in-out max-w-xs sm:max-w-none mx-auto" data-animate="slideInUp" data-delay="0.1s">
                        <div class="relative w-full aspect-ratio-9-16 mb-4">
                            <img src="C:\Users\mahom\OneDrive\Documents\javandzalo\4273131e-0caa-4f20-8df0-05514d0f0d12.png" alt="Product Image 2" class="absolute inset-0 w-full h-full object-cover rounded-lg shadow-md sm:w-[90%] sm:mx-auto">
                        </div>
                        <div class="p-6 text-center">
                            <h3 class="text-xl font-semibold mb-2 text-gray-900">Smart Home Hub</h3>
                            <p class="text-gray-600 text-sm mb-4">Control your home with ease.</p>
                            <div class="flex justify-center items-center">
                                <button class="btn-primary bg-indigo-600 text-white px-5 py-2 rounded-full text-sm font-medium hover:bg-indigo-700">
                                    View Details
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Product Card 3 -->
                    <div class="product-card bg-gray-50 rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 ease-in-out max-w-xs sm:max-w-none mx-auto" data-animate="slideInUp" data-delay="0.2s">
                        <div class="relative w-full aspect-ratio-9-16 mb-4">
                            <img src="C:\Users\mahom\OneDrive\Documents\javandzalo\7e569756-bc34-40ca-9a40-f08c6d10c7e6.png" alt="Product Image 3" class="absolute inset-0 w-full h-full object-cover rounded-lg shadow-md sm:w-[90%] sm:mx-auto">
                        </div>
                        <div class="p-6 text-center">
                            <h3 class="text-xl font-semibold mb-2 text-gray-900">Ergonomic Workspace</h3>
                            <p class="text-gray-600 text-sm mb-4">Comfort and productivity combined.</p>
                            <div class="flex justify-center items-center">
                                <button class="btn-primary bg-indigo-600 text-white px-5 py-2 rounded-full text-sm font-medium hover:bg-indigo-700">
                                    View Details
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Product Card 4 - Using a placeholder as only 3 product images were provided -->
                    <div class="product-card bg-gray-50 rounded-xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300 ease-in-out max-w-xs sm:max-w-none mx-auto" data-animate="slideInUp" data-delay="0.3s">
                        <div class="relative w-full aspect-ratio-9-16 mb-4">
                            <img src="https://placehold.co/600x1066/a5b4fc/ffffff?text=Product+4" alt="Product Image 4" class="absolute inset-0 w-full h-full object-cover rounded-lg shadow-md sm:w-[90%] sm:mx-auto">
                        </div>
                        <div class="p-6 text-center">
                            <h3 class="text-xl font-semibold mb-2 text-gray-900">Portable Power Bank</h3>
                            <p class="text-gray-600 text-sm mb-4">Power on the go, always connected.</p>
                            <div class="flex justify-center items-center">
                                <button class="btn-primary bg-indigo-600 text-white px-5 py-2 rounded-full text-sm font-medium hover:bg-indigo-700">
                                    View Details
                                </button>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="text-center mt-12" data-animate="popIn" data-delay="0.4s">
                    <a href="#" class="btn-primary inline-block bg-indigo-500 text-white hover:bg-indigo-600 px-8 py-4 rounded-full text-lg font-semibold shadow-lg">
                        View All Products
                    </a>
                </div>
            </div>
        </section>

        <!-- About Us / Features Section -->
        <section id="about" class="py-16 md:py-24 bg-gradient-to-br from-indigo-50 to-purple-50">
            <div class="container mx-auto px-6 flex flex-col md:flex-row items-center gap-12">
                <div class="md:w-1/2 text-center md:text-left">
                    <h2 class="text-3xl md:text-4xl font-bold mb-6 text-gray-900" data-animate="slideInLeft">Our Commitment to Excellence</h2>
                    <p class="text-lg text-gray-700 leading-relaxed mb-6" data-animate="slideInLeft" data-delay="0.1s">
                        At YourBrand, we believe in bringing you the future, today. We meticulously curate a collection of innovative products that are not just high-tech, but also seamlessly integrate into your lifestyle, making it simpler, smarter, and more enjoyable.
                    </p>
                    <ul class="list-disc list-inside text-gray-700 space-y-2 text-lg" data-animate="slideInLeft" data-delay="0.2s">
                        <li>High-Quality, Tested Products</li>
                        <li>Customer-Centric Support</li>
                        <li>Fast & Reliable Shipping</li>
                        <li>Secure Shopping Experience</li>
                    </ul>
                </div>
                <div class="md:w-1/2" data-animate="slideInRight">
                    <!-- Using a placeholder for the about us image as no specific image was provided for it -->
                    <img src="https://placehold.co/800x600/6366f1/ffffff?text=Innovation" alt="About Us Image" class="rounded-xl shadow-2xl w-full h-auto object-cover transform hover:scale-105 transition-transform duration-500 ease-in-out">
                </div>
            </div>
        </section>

        <!-- Call to Action Section -->
        <section class="py-16 md:py-24 bg-indigo-700 text-white text-center">
            <div class="container mx-auto px-6">
                <h2 class="text-3xl md:text-5xl font-bold mb-6 leading-tight drop-shadow-lg" data-animate="scaleIn">
                    Don't Miss Out on the Future!
                </h2>
                <p class="text-lg md:text-xl max-w-3xl mx-auto mb-10 opacity-90" data-animate="fadeIn" data-delay="0.1s">
                    Sign up for our newsletter to get exclusive deals, early access to new products, and tech insights delivered straight to your inbox.
                </p>
                <form class="max-w-md mx-auto flex flex-col sm:flex-row gap-4" data-animate="slideInUp" data-delay="0.2s">
                    <input type="email" placeholder="Enter your email address" class="flex-grow p-4 rounded-full border-2 border-white focus:outline-none focus:ring-2 focus:ring-indigo-300 text-gray-900 placeholder-gray-500 shadow-inner">
                    <button type="submit" class="btn-primary bg-white text-indigo-700 hover:bg-gray-100 px-8 py-4 rounded-full text-lg font-semibold shadow-xl">
                        Subscribe Now
                    </button>
                </form>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer id="contact" class="bg-gray-900 text-gray-300 py-12 md:py-16">
        <div class="container mx-auto px-6 grid grid-cols-1 md:grid-cols-3 gap-10">
            <!-- Brand Info -->
            <div class="col-span-1" data-animate="fadeIn" data-delay="0s">
                <h3 class="text-2xl font-bold text-white mb-4">YourBrand</h3>
                <p class="text-sm leading-relaxed">
                    Bringing you the best of innovation and quality. Your trusted source for modern products.
                </p>
                <div class="flex space-x-4 mt-6">
                    <!-- Placeholder social icons -->
                    <a href="#" class="text-gray-400 hover:text-white transition duration-200"><img src="https://placehold.co/24x24/3b82f6/ffffff?text=F" alt="Facebook" class="h-6 w-6"></a>
                    <a href="#" class="text-gray-400 hover:text-white transition duration-200"><img src="https://placehold.co/24x24/1da1f2/ffffff?text=T" alt="Twitter" class="h-6 w-6"></a>
                    <a href="#" class="text-gray-400 hover:text-white transition duration-200"><img src="https://placehold.co/24x24/e1306c/ffffff?text=I" alt="Instagram" class="h-6 w-6"></a>
                </div>
            </div>

            <!-- Quick Links -->
            <div class="col-span-1" data-animate="fadeIn" data-delay="0.1s">
                <h3 class="text-xl font-semibold text-white mb-4">Quick Links</h3>
                <ul class="space-y-2">
                    <li><a href="#home" class="text-gray-400 hover:text-white transition duration-200">Home</a></li>
                    <li><a href="#products" class="text-gray-400 hover:text-white transition duration-200">Shop</a></li>
                    <li><a href="#about" class="text-gray-400 hover:text-white transition duration-200">About Us</a></li>
                    <li><a href="#contact" class="text-gray-400 hover:text-white transition duration-200">Contact</a></li>
                </ul>
            </div>

            <!-- Contact Info -->
            <div class="col-span-1" data-animate="fadeIn" data-delay="0.2s">
                <h3 class="text-xl font-semibold text-white mb-4">Contact Us</h3>
                <p class="text-sm">Email: <a href="mailto:info@yourbrand.com" class="text-gray-400 hover:text-white">info@yourbrand.com</a></p>
                <p class="text-sm mt-2">Phone: <a href="tel:+1234567890" class="text-gray-400 hover:text-white">+1 (234) 567-890</a></p>
                <p class="text-sm mt-2">Address: 123 Innovation Drive, Tech City, TX 78901</p>
                <p class="text-sm mt-4">&copy; 2025 YourBrand. All rights reserved.</p>
                <p class="text-sm mt-1">
                    <a href="#" class="text-gray-400 hover:text-white mr-4">Privacy Policy</a>
                    <a href="#" class="text-gray-400 hover:text-white">Terms of Service</a>
                </p>
            </div>
        </div>
    </footer>

    <script>
        // JavaScript for sticky header and mobile menu
        document.addEventListener('DOMContentLoaded', () => {
            const header = document.getElementById('main-header');
            const mobileMenuButton = document.getElementById('mobile-menu-button');
            const mobileMenu = document.getElementById('mobile-menu');
            const closeMenuButton = document.getElementById('close-menu-button');
            const heroBgImage = document.getElementById('hero-bg-image'); // Get the hero background image

            // Sticky header effect
            window.addEventListener('scroll', () => {
                if (window.scrollY > 50) {
                    header.classList.add('scrolled');
                } else {
                    header.classList.remove('scrolled');
                }

                // Parallax effect for hero background image
                if (heroBgImage) {
                    const scrollY = window.scrollY;
                    // Adjust the multiplier (0.2) to control the parallax speed
                    // This now adds to the base -50% transform
                    heroBgImage.style.transform = `translate(-50%, calc(-50% + ${scrollY * 0.2}px))`;
                }
            });

            // Mobile menu toggle
            function toggleMobileMenu() {
                mobileMenu.classList.toggle('hidden');
                mobileMenu.classList.toggle('translate-x-full');
                mobileMenu.classList.toggle('translate-x-0');
                mobileMenuButton.classList.toggle('open'); // Toggle hamburger icon animation
            }

            mobileMenuButton.addEventListener('click', toggleMobileMenu);
            closeMenuButton.addEventListener('click', toggleMobileMenu);

            // Intersection Observer for scroll animations
            const animatedElements = document.querySelectorAll('[data-animate]');

            const appearOptions = {
                threshold: 0.1, // Trigger when 10% of the element is visible
                rootMargin: "0px 0px -50px 0px" // Shrink the viewport by 50px from bottom
            };

            const appearOnScroll = new IntersectionObserver(function(entries, observer) {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const animationClass = `animate-${entry.target.dataset.animate}`;
                        const delay = entry.target.dataset.delay || '0s'; // Default to 0s if no delay specified

                        entry.target.style.animationDelay = delay;
                        entry.target.classList.add(animationClass);
                        entry.target.style.opacity = 1; // Ensure opacity is set for non-fade animations
                        observer.unobserve(entry.target); // Stop observing once animated
                    }
                });
            }, appearOptions);

            animatedElements.forEach(element => {
                appearOnScroll.observe(element);
            });
        });
    </script>
</body>
</html>

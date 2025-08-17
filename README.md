<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Vastra - Online Shopping</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    .product-card {
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .product-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    }
    #loading {
      display: none;
      text-align: center;
      padding: 20px;
      color: #666;
    }
  </style>
</head>
<body class="bg-gray-50 min-h-screen">
  <!-- Header -->
  <header class="bg-white shadow-sm border-b">
    <div class="px-4 py-3">
      <div class="flex items-center justify-between mb-4">
        <div class="flex items-center space-x-3">
          <img src="https://placehold.co/40x40/6366f1/ffffff?text=VK" alt="Profile" class="w-10 h-10 rounded-full">
          <span class="font-medium text-gray-800">Vastra User</span>
        </div>
        <div class="flex items-center space-x-4">
          <button class="p-2 text-gray-600 hover:text-red-500 transition-colors">
            <i class="fas fa-heart w-6 h-6"></i>
          </button>
          <button class="relative p-2 text-gray-600 hover:text-red-500 transition-colors">
            <i class="fas fa-shopping-cart w-6 h-6"></i>
            <span class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center">0</span>
          </button>
        </div>
      </div>

      <form class="mb-4">
        <div class="relative">
          <input type="text" placeholder="Search by Keyword or Product ID" class="w-full px-4 py-3 pl-10 pr-12 rounded-full border border-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent">
          <button type="submit" class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400">
            <i class="fas fa-search w-5 h-5"></i>
          </button>
          <button type="button" class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-400">
            <i class="fas fa-camera w-5 h-5"></i>
          </button>
        </div>
      </form>

      <div class="flex items-center text-sm text-gray-600 mb-4">
        <i class="fas fa-map-marker-alt w-5 h-5 mr-2"></i>
        <span>Delivering to India</span>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <main class="max-w-screen-lg mx-auto px-4 pb-20">
    <!-- Banner -->
    <div class="mb-6">
      <div class="bg-gradient-to-r from-yellow-400 to-orange-500 rounded-lg overflow-hidden shadow-lg">
        <div class="p-4 text-center">
          <h3 class="text-white font-bold text-lg">SUMMER SALE</h3>
          <p class="text-white text-2xl font-extrabold">UP TO 50% OFF</p>
        </div>
      </div>
    </div>

    <!-- Products Grid (2 per row) -->
    <div id="products-container" class="space-y-6">
      <!-- Products will be loaded here -->
    </div>

    <!-- Loading Spinner -->
    <div id="loading" class="text-center py-6">
      <i class="fas fa-spinner fa-spin text-2xl text-purple-600"></i>
      <p class="mt-2">Loading more products...</p>
    </div>
  </main>

  <!-- Bottom Navigation -->
  <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200 px-4 py-2">
    <div class="flex justify-around">
      <button class="flex flex-col items-center py-2 text-purple-600">
        <i class="fas fa-home text-xl"></i>
        <span class="text-xs mt-1">Home</span>
      </button>
      <button class="flex flex-col items-center py-2 text-gray-500 hover:text-purple-600 transition-colors">
        <i class="fas fa-search text-xl"></i>
        <span class="text-xs mt-1">Search</span>
      </button>
      <button class="flex flex-col items-center py-2 text-gray-500 hover:text-purple-600 transition-colors">
        <i class="fas fa-plus-circle text-xl"></i>
        <span class="text-xs mt-1">Add</span>
      </button>
      <button class="flex flex-col items-center py-2 text-gray-500 hover:text-purple-600 transition-colors">
        <i class="fas fa-shopping-bag text-xl"></i>
        <span class="text-xs mt-1">Orders</span>
      </button>
      <button class="flex flex-col items-center py-2 text-gray-500 hover:text-purple-600 transition-colors">
        <i class="fas fa-user text-xl"></i>
        <span class="text-xs mt-1">Account</span>
      </button>
    </div>
  </nav>

  <script>
    // Sample product data
    const products = [
      { name: "Designer Saree", image: "https://placehold.co/300x300/ec4891/ffffff?text=Saree", price: "₹899", original: "₹1299", discount: "35% OFF", rating: "4.7", reviews: "892" },
      { name: "Casual Shoes", image: "https://placehold.co/300x300/f59e0b/ffffff?text=Shoes", price: "₹499", original: "₹699", discount: "35% OFF", rating: "4.2", reviews: "3456" },
      { name: "Men's Cotton Shirt", image: "https://placehold.co/300x300/f59e0b/ffffff?text=Shirt", price: "₹399", original: "₹499", discount: "20% OFF", rating: "4.2", reviews: "1234" },
      { name: "Women's Summer Dress", image: "https://placehold.co/300x300/ec4891/ffffff?text=Dress", price: "₹599", original: "₹699", discount: "15% OFF", rating: "4.5", reviews: "2345" },
      { name: "Slim Fit Jeans", image: "https://placehold.co/300x300/10b981/ffffff?text=Jeans", price: "₹799", original: "₹999", discount: "25% OFF", rating: "4.3", reviews: "3456" },
      { name: "Men's Winter Jacket", image: "https://placehold.co/300x300/8b5cf6/ffffff?text=Jacket", price: "₹1199", original: "₹1699", discount: "30% OFF", rating: "4.7", reviews: "1567" },
      { name: "Premium Men's Jacket", image: "https://placehold.co/300x300/10b981/ffffff?text=Jacket", price: "₹599", original: "₹799", discount: "35% OFF", rating: "4.5", reviews: "1567" },
      { name: "Stylish Women's Dress", image: "https://placehold.co/300x300/f59e0b/ffffff?text=Dress", price: "₹349", original: "₹420", discount: "17% OFF", rating: "4.3", reviews: "2345" }
    ];

    let currentIndex = 0;
    const productsPerLoad = 2; // Load 2 products at a time
    const container = document.getElementById("products-container");
    const loading = document.getElementById("loading");

    // Function to render 2 products in a row
    function renderProductRow(startIndex) {
      const row = document.createElement("div");
      row.className = "grid grid-cols-1 sm:grid-cols-2 gap-6";

      for (let i = startIndex; i < startIndex + 2 && i < products.length; i++) {
        const p = products[i];
        const card = document.createElement("div");
        card.className = "bg-white rounded-xl shadow-md overflow-hidden product-card";
        card.innerHTML = `
          <div class="relative">
            <img src="${p.image}" alt="${p.name}" class="w-full h-48 object-cover">
            <div class="absolute top-2 left-2 bg-red-500 text-white text-xs font-bold px-2 py-1 rounded">${p.discount}</div>
          </div>
          <div class="p-4">
            <h3 class="font-medium text-gray-800 mb-2">${p.name}</h3>
            <div class="flex items-center mb-2">
              <div class="flex items-center bg-green-100 px-2 py-1 rounded">
                <i class="fas fa-star text-yellow-400 text-xs"></i>
                <span class="text-xs font-bold text-gray-700 ml-1">${p.rating}</span>
              </div>
              <span class="text-xs text-gray-500 ml-2">(${p.reviews})</span>
            </div>
            <div class="flex items-center justify-between mb-3">
              <div>
                <span class="text-lg font-bold text-gray-800">${p.price}</span>
                <span class="text-sm text-gray-500 line-through ml-2">${p.original}</span>
              </div>
            </div>
            <button class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-2 px-4 rounded-lg transition-colors">
              ADD TO CART
            </button>
          </div>
        `;
        row.appendChild(card);
      }

      container.appendChild(row);
    }

    // Load initial products
    function loadInitialProducts() {
      renderProductRow(currentIndex);
      currentIndex += 2;
    }

    // Load more on scroll
    function loadMoreProducts() {
      if (currentIndex >= products.length) {
        window.removeEventListener("scroll", handleScroll);
        return;
      }

      loading.style.display = "block";
      setTimeout(() => {
        renderProductRow(currentIndex);
        currentIndex += 2;
        loading.style.display = "none";
      }, 800); // Simulate loading delay
    }

    // Scroll handler
    function handleScroll() {
      if (window.innerHeight + window.scrollY >= document.body.offsetHeight - 1000) {
        loadMoreProducts();
      }
    }

    // Initialize
    loadInitialProducts();
    window.addEventListener("scroll", handleScroll);
  </script>
</body>
</html>

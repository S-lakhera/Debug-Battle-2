In server

1. connectDB() function is called before the configuration of dotenv
2. multer is used but package name not available in package.json
   so I installed using "npm install multer"

3. Added all required values in .env file
4. Password is sent in register and login controller in response
5. Removed "/" from allowed origin in cors configuration 
6. Updated "process.env.JWT_SECRET" in authMiddleware
7. Updated logic of checking inventoryStock before placing order in orderController at line no 127




In Frontend 
1. In login form the name of password input was "pass" it should be "password"
2. In axios.js added "baseURL: import.meta.env.VITE_API_URL || 'http://localhost:3000/api'," also updated line no 34
3. In dashboard.jsx line no. 231 updated endpoint from "/product" to "/products"
4. In dashboard.jsx line no. 308 updated endpoint from "/order" to "/orders"
5. Removed variant="outline" from multiple places in Dashboard.jsx
6. Updated text-zinc-400, Updated text-zinc-200  at multiple lines in dashboard.jsx
 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>G18 Product Store</title>

<style>
    *{
        margin:0;
        padding:0;
        box-sizing:border-box;
        font-family:Arial, sans-serif;
    }

    body{
        background:#0f172a;
        color:white;
    }

    header{
        background:#111827;
        padding:20px;
        text-align:center;
        font-size:30px;
        font-weight:bold;
        letter-spacing:2px;
        box-shadow:0 0 10px rgba(0,0,0,0.5);
    }

    .container{
        width:90%;
        max-width:1200px;
        margin:auto;
        padding:20px;
    }

    .admin-panel{
        background:#1e293b;
        padding:20px;
        border-radius:15px;
        margin-bottom:30px;
    }

    .admin-panel h2{
        margin-bottom:15px;
    }

    input{
        width:100%;
        padding:12px;
        margin:10px 0;
        border:none;
        border-radius:10px;
        outline:none;
    }

    button{
        background:#22c55e;
        color:white;
        border:none;
        padding:12px 20px;
        border-radius:10px;
        cursor:pointer;
        font-size:16px;
        transition:0.3s;
    }

    button:hover{
        background:#16a34a;
    }

    .products{
        display:grid;
        grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
        gap:20px;
    }

    .card{
        background:#1e293b;
        padding:20px;
        border-radius:15px;
        text-align:center;
        transition:0.3s;
    }

    .card:hover{
        transform:translateY(-5px);
    }

    .price{
        color:#22c55e;
        font-size:24px;
        margin:10px 0;
    }

    .delete-btn{
        background:red;
        margin-top:10px;
    }
</style>
</head>

<body>

<header>
    G18 PRODUCT STORE
</header>

<div class="container">

    <!-- Admin Panel -->
    <div class="admin-panel">
        <h2>Admin Panel</h2>

        <input type="text" id="productName" placeholder="Enter Product Name">
        <input type="number" id="productPrice" placeholder="Enter Product Price">

        <button onclick="addProduct()">Add Product</button>
    </div>

    <!-- Product List -->
    <div class="products" id="productList"></div>

</div>

<script>

let products = JSON.parse(localStorage.getItem("products")) || [];

function saveProducts(){
    localStorage.setItem("products", JSON.stringify(products));
}

function displayProducts(){

    let productList = document.getElementById("productList");
    productList.innerHTML = "";

    products.forEach((product, index)=>{

        productList.innerHTML += `
            <div class="card">
                <h2>${product.name}</h2>
                <div class="price">Rs. ${product.price}</div>

                <button class="delete-btn" onclick="deleteProduct(${index})">
                    Delete
                </button>
            </div>
        `;
    });

}

function addProduct(){

    let name = document.getElementById("productName").value;
    let price = document.getElementById("productPrice").value;

    if(name === "" || price === ""){
        alert("Please fill all fields");
        return;
    }

    products.push({
        name:name,
        price:price
    });

    saveProducts();
    displayProducts();

    document.getElementById("productName").value = "";
    document.getElementById("productPrice").value = "";

}

function deleteProduct(index){

    products.splice(index,1);

    saveProducts();
    displayProducts();

}

displayProducts();

</script>

</body>
</html># My-site

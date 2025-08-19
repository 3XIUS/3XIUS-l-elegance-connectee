// Charger le panier depuis localStorage
let cart = JSON.parse(localStorage.getItem("cart")) || [];

// Ajouter un produit au panier
document.querySelectorAll(".add-to-cart").forEach(button => {
  button.addEventListener("click", () => {
    let name = button.dataset.name;
    let price = parseFloat(button.dataset.price);

    cart.push({ name, price });
    localStorage.setItem("cart", JSON.stringify(cart));

    alert(`${name} ajouté au panier !`);
  });
});

// Afficher le panier sur la page cart.html
if (document.getElementById("cart-table")) {
  let tbody = document.querySelector("#cart-table tbody");
  let total = 0;

  cart.forEach((item, index) => {
    let row = document.createElement("tr");

    row.innerHTML = `
      <td>${item.name}</td>
      <td>${item.price} €</td>
      <td><button class="remove" data-index="${index}">Retirer</button></td>
    `;

    tbody.appendChild(row);
    total += item.price;
  });

  document.getElementById("total").textContent = total;

  // Retirer un produit
  document.querySelectorAll(".remove").forEach(button => {
    button.addEventListener("click", () => {
      let index = button.dataset.index;
      cart.splice(index, 1);
      localStorage.setItem("cart", JSON.stringify(cart));
      location.reload();
    });
  });
}

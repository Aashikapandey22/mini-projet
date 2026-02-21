let books = JSON.parse(localStorage.getItem("books")) || [];
let editId = null;
/* ---------- helpers ---------- */
function uid() {
    return Date.now() + Math.random().toString(16).slice(2);
}
function save() {
    localStorage.setItem("books", JSON.stringify(books));
}
function categoryColor(cat) {
    const map = {
        Fiction: "#6366f1",
        Tech: "#10b981",
        History: "#f59e0b",
        Science: "#ef4444"
    };
    return map[cat] || "#6b7280";
}
/* ---------- add/update ---------- */
function addOrUpdateBook() {
    const title = titleInput.value.trim();
    const author = authorInput.value.trim();
    const category = categoryInput.value;
    if (!title || !author || !category) {
        alert("Fill all fields");
        return;
    }
    if (editId) {
        const b = books.find(x => x.id === editId);
        b.title = title;
        b.author = author;
        b.category = category;
        editId = null;
        modeLabel.innerText = "";
    } 
    else {
        books.push({
            id: uid(),
            title,
            author,
            category,
            fav: false,
            created: Date.now()
        });
    }
    clearForm();
    save();
    render();
}
/* ---------- edit ---------- */
function editBook(id) {
    const b = books.find(x => x.id === id);
    if (!b) return;
    titleInput.value = b.title;
    authorInput.value = b.author;
    categoryInput.value = b.category;
    editId = id;
    modeLabel.innerText = "Editing book...";
    titleInput.focus();
}
/* ---------- delete ---------- */
function deleteBook(id) {
    if (!confirm("Delete this book?")) return;
    books = books.filter(b => b.id !== id);
    save();
    render();
}
/* ---------- favorite ---------- */
function toggleFav(id) {
    const b = books.find(x => x.id === id);
    b.fav = !b.fav;
    save();
    render();
}
/* ---------- search ---------- */

function searchBooks() {
    render(searchInput.value.toLowerCase());
}
/* ---------- sort ---------- */
function sortBooks() {
    const key = sortSelect.value;
    if (!key) return render();

    books.sort((a,b) => a[key].localeCompare(b[key]));
    render();
}
/* ---------- render ---------- */
function render(searchKey = "") {
    bookList.innerHTML = "";
    let list = books.filter(b =>
        b.title.toLowerCase().includes(searchKey) ||
        b.author.toLowerCase().includes(searchKey) ||
        b.category.toLowerCase().includes(searchKey)
    );
    if (!list.length) {
        bookList.innerHTML = "<p>No books found</p>";
    }
    list.forEach(b => {
        const div = document.createElement("div");
        div.className = "book";
        div.innerHTML = `
            <div><strong>${b.title}</strong> ${b.fav ? "⭐" : ""}</div>
            <div>${b.author}</div>
            <span class="badge" style="background:${categoryColor(b.category)}">
                ${b.category}
            </span>
            <div class="actions">
                <button onclick="editBook('${b.id}')">Edit</button>
                <button onclick="deleteBook('${b.id}')">Delete</button>
                <button onclick="toggleFav('${b.id}')">Fav</button>
            </div>
        `;
        bookList.appendChild(div);
    });
    bookCount.innerText = "Total Books: " + books.length;
}
/* ---------- import/export ---------- */
function exportData() {
    const blob = new Blob([JSON.stringify(books)], {type:"application/json"});
    const a = document.createElement("a");
    a.href = URL.createObjectURL(blob);
    a.download = "books.json";
    a.click();
}
importFile.onchange = e => {
    const file = e.target.files[0];
    const reader = new FileReader();
    reader.onload = () => {
        books = JSON.parse(reader.result);
        save();
        render();
    };
    reader.readAsText(file);
};
/* ---------- theme ---------- */
themeToggle.onclick = () => {
    document.body.classList.toggle("dark");
    localStorage.setItem("theme",
        document.body.classList.contains("dark") ? "dark":"light");
};
if (localStorage.getItem("theme") === "dark") {
    document.body.classList.add("dark");
}
/* ---------- misc ---------- */
function clearForm() {
    titleInput.value = "";
    authorInput.value = "";
    categoryInput.value = "";
}

titleInput.addEventListener("keydown", e => {
    if (e.key === "Enter") addOrUpdateBook();
});
/* ---------- start ---------- */
render();

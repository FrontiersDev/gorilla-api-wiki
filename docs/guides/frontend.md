# Website Integration

You can fetch data from the API using standard JavaScript `fetch`. This is useful for building fan sites, wikis, or trade calculators.

## Fetch & Display

```javascript
async function loadGallery() {
    try {
        const response = await fetch('http://localhost:3000/api/cosmetics');
        const data = await response.json();

        const container = document.getElementById('gallery');

        data.items.forEach(item => {
            const div = document.createElement('div');
            div.innerHTML = `
                <h3>${item.name}</h3>
                <img src="http://localhost:3000/assets/icons/${item.files.icon}" width="100">
                <p>${item.price} Rocks</p>
            `;
            container.appendChild(div);
        });

    } catch (error) {
        console.error("Failed to load cosmetics", error);
    }
}

loadGallery();
```
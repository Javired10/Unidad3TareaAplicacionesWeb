<template>
    <div class="product-card">
        <img :src="product.imageUrl" :alt="product.nombre" class="product-image" />
        <div class="product-info">
            <h3>{{ product.nombre }}</h3>
            <p class="category">{{ product.categoryId?.nombre || 'Sin categoría' }}</p>
            <p class="price">${{ product.precio.toFixed(2) }}</p>
            <p class="stock">Stock: {{ product.stock }}</p>
            <button @click="$emit('added-to-cart', product)" :disabled="product.stock <= 0">
                {{ product.stock <= 0 ? 'Agotado' : 'Añadir al Carrito' }}
            </button>
        </div>
    </div>
</template>

<script setup>
defineProps({
    product: {
        type: Object,
        required: true
    }
});

defineEmits(['added-to-cart']);
</script>

<style scoped>
.product-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 16px;
    text-align: center;
    transition: transform 0.2s, box-shadow 0.2s;
    background: white;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.product-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
}

.product-image {
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 4px;
    margin-bottom: 12px;
}

.product-info h3 {
    margin: 0 0 8px 0;
    font-size: 1.2rem;
}

.category {
    font-size: 0.85rem;
    color: #666;
    margin-bottom: 8px;
}

.price {
    font-weight: bold;
    font-size: 1.1rem;
    color: #2c3e50;
    margin-bottom: 8px;
}

.stock {
    font-size: 0.9rem;
    margin-bottom: 12px;
}

button {
    background-color: #42b983;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
    transition: background 0.2s;
}

button:hover:not(:disabled) {
    background-color: #3aa876;
}

button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}
</style>

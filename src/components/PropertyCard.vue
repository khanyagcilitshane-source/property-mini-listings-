<template>
    <div class="card">

        <span
        v-if="!property.available"
        class="badge">
        Not Available
        </span>

        <img :src="property.image" :alt="property.title">

        <div class="content">
            <h3>{{ property.title }}</h3>

            <p>📍 {{ property.location }}</p>

            <p><strong>R{{ property.price }}/night</strong></p>

            <p>🏠 {{ property.type }}</p>

            <p v-if="property.available" class="available">
                Available
            </p>

            <button @click="$emit('toggle-favourite', property.id)">
                {{ property.favourite ? '❤️ Saved' : '🤍 Save'  }}
            </button>
        </div>

    </div>
</template>

<script>
export default {
    props: ["property"]
}
</script>

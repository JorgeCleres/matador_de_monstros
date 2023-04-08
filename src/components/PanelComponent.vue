<template>
    <div class="score">
        <h1>{{ title }}</h1>
        <div class="life-bar">
            <div class="life"
                :class="{danger : life < 20}"
                :style="{width: life + '%'}"
            ></div>
        </div>
        <div>{{ life }}%</div>
    </div>
</template>

<script>
export default {
    //props: ['title', 'life']
    props: {
        title: {
            type: String,
            default: 'sem nome',
            required: true
        },
        life: {
            type: Number,
            default: 100,
            required: true
        }
    }
}
</script>

<style>

    .panel {
		margin: 10px;
		padding: 20px;
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
	}

</style>
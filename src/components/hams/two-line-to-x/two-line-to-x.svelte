<script lang="ts">
    export let isMenuOpen: boolean = false;
</script>

<input bind:checked={isMenuOpen} class="two-line-to-x-ham-trigger" type="checkbox" />

<style lang="scss">
    @import "./two-line-to-x.scss";
</style>
<template>
    <div class="rounded-xl relative overflow-hidden" :class="[paddingY, paddingX, backgroundColor, width]">
        <button class="scroll-btn scroll-left disabled:opacity-25 disabled:cursor-not-allowed" :disabled="!canScrollLeft"
            @click="scrollLeft">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"
                stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
            </svg>
        </button>
        <div ref="element" class="h-full whitespace-nowrap wa-scrollbar flex overflow-hidden" @scroll="updateCanScroll">
            <slot></slot>
        </div>
        <button class="scroll-btn scroll-right disabled:opacity-25 disabled:cursor-not-allowed" :disabled="!canScrollRight"
            @click="scrollRight">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"
                stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
            </svg>
        </button>
    </div>
</template>

<script>
import anime from 'animejs/lib/anime.es';

export default {
    props: {
        paddingY: {
            type: String,
            default: 'py-4',
        },
        paddingX: {
            type: String,
            default: 'px-7',
        },
        backgroundColor: {
            type: String,
            default: 'bg-gray-200',
        },
        width: {
            type: String,
            default: '',
        },
    },
    data() {
        return {
            isDisabled: false,
            cardSpacing: 8,
            canScrollLeft: false,
            canScrollRight: false,
            cardWidth: 0,
            columns: 3,
            observer: null,
        };
    },
    computed: {
        element() {
            return this.$refs.element;
        },
    },
    mounted() {
        const totalSpaces = this.columns - 1;
        this.cardWidth =
            (this.element.clientWidth - this.cardSpacing * totalSpaces) /
            this.columns;
        this.$nextTick(this.updateCanScroll());

        // observe mutations on slot
        this.observer = new MutationObserver(this.updateCanScroll);
        this.observer.observe(this.$refs.element, {
            childList: true,
            attributes: false,
            subtree: true,
        });
    },
    destroyed() {
        this.observer.disconnect();
    },
    methods: {
        scrollLeft() {
            anime({
                targets: this.element,
                scrollLeft:
                    this.element.scrollLeft - (this.cardWidth + this.cardSpacing),
                duration: 500,
                easing: 'easeInOutQuad',
            });
        },

        scrollRight() {
            anime({
                targets: this.element,
                scrollLeft:
                    this.element.scrollLeft + (this.cardWidth + this.cardSpacing),
                duration: 500,
                easing: 'easeInOutQuad',
            });
        },
        updateCanScroll() {
            this.canScrollLeft = this.$refs.element.scrollLeft > 0;
            this.canScrollRight =
                Math.ceil(this.$refs.element.scrollLeft) <
                this.$refs.element.scrollWidth - this.$refs.element.offsetWidth;
        },
    },
};
</script>

<style scoped>
.scroll-btn {
    @apply absolute w-5 h-full top-0 bg-black z-10 flex items-center justify-center;
}

.scroll-btn.scroll-left {
    @apply absolute left-0 rounded-l-[10px];
}

.scroll-btn.scroll-right {
    @apply absolute right-0 rounded-r-[10px];
}
</style>
<!-- active:bg-gray-700 -->
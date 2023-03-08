<script lang="ts">
    import p5 from "p5";
    import { onMount } from "svelte";
    let mainDiv: HTMLDivElement;

    const s = (p: p5) => {
        let x = 100;
        let y = 100;

        p.setup = function () {
            p.createCanvas(mainDiv.clientWidth, mainDiv.clientHeight);
        };

        p.draw = function () {
            p.background(255);
            p.fill("red");
            p.noStroke();
            p.rect(x, y, 50, 50);
        };

        p.windowResized = function () {
            p.resizeCanvas(mainDiv.clientWidth, mainDiv.clientHeight);
        };
    };

    onMount(() => {
        new p5(s, mainDiv);
    });
</script>

<div bind:this={mainDiv}>
    <slot />
</div>

<style>
    :global(div .p5Canvas) {
        position: absolute;
        top: 0;
        left: 0;
        z-index: -100;
    }
</style>

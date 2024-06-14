<template>
    <div>
        <div id="viewer"></div>
    </div>
</template>

<script setup lang="ts">
import { onMounted } from "vue";
import perspective from "@finos/perspective";
import "@finos/perspective-viewer";
import "@finos/perspective-viewer-datagrid";
import "@finos/perspective-viewer-d3fc";
import "@finos/perspective-viewer/dist/css/pro.css";

const createTable = async () => {
    const worker = perspective.worker();
    const viewer: any = document.createElement("perspective-viewer");
    document.getElementById("viewer").appendChild(viewer);

    let REQ = fetch("https://api.covidtracking.com/v1/states/daily.csv");

    const resp = await REQ;
    const csv = await resp.text();

    const table = await worker.table(csv);
    console.log(table);
    viewer.load(table);
};

onMounted(() => {
    createTable();
});
</script>

<style>
perspective-viewer {
    position: absolute;
    top: 16px;
    left: 16px;
    right: 16px;
    bottom: 16px;
}
</style>

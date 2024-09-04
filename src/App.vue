<script setup lang="ts">
import {useStorageAsync} from "@vueuse/core";

import type {StorageLikeAsync} from "@vueuse/core"


const storage: StorageLikeAsync = {
    async getItem(key: string): Promise<string | null> {
        console.log("getItem");
        const {promise, resolve} = Promise.withResolvers<string | null>();
        setTimeout(() => {
            resolve(localStorage.getItem(key));
        }, 10);
        return promise;
    },

    async setItem(key: string, value: string): Promise<void> {
        console.log("setItem");
        const {promise, resolve} = Promise.withResolvers<void>();
        setTimeout(() => {
            localStorage.setItem(key, value);
            resolve();
        }, 10);
        return promise;
    },

    async removeItem(key: string): Promise<void> {
        console.log("removeItem");
        const {promise, resolve} = Promise.withResolvers<void>();
        setTimeout(() => {
            localStorage.removeItem(key);
            resolve();
        }, 10);
        return promise;
    }
} as StorageLikeAsync;

const text = useStorageAsync("data", "init", storage, {
    listenToStorageChanges: true,
    writeDefaults: true
});
</script>

<template>
    <input type="text" v-model="text"/>
</template>

<style scoped>

</style>

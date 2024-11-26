<script setup lang="ts">
import { ref } from "vue";
import CommonButton from "./components/common/button.vue";

// Task 인터페이스 정의
interface Task {
    text: string;
    completed: boolean;
}

const tasks = ref<Task[]>([]); // Task 배열
const newTask = ref<string>(""); // 새로운 Task 입력 값

// 새로운 Task 추가
const addTask = (): void => {
    if (newTask.value.trim() === "") return;
    tasks.value.push({ text: newTask.value.trim(), completed: false });
    newTask.value = "";
};

// Task 완료 상태 토글
const toggleTask = (index: number): void => {
    tasks.value[index].completed = !tasks.value[index].completed;
};

// Task 삭제
const deleteTask = (index: number): void => {
    tasks.value.splice(index, 1);
};
</script>

<template>
    <div class="min-h-screen bg-gray-100 flex items-center justify-center p-5">
        <div class="bg-white rounded-lg shadow-lg p-6 w-full max-w-md">
            <h1 class="text-2xl font-bold mb-4 text-center">To-Do List</h1>
            <form @submit.prevent="addTask" class="flex mb-4">
                <input
                    v-model="newTask"
                    type="text"
                    placeholder="Add a new Task"
                    class="flex-grow p-2 border rounded-l-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                />
                <common-button
                    label="Add Task"
                    type="primary"
                    :disabled="newTask.trim() === ''"
                    @click="addTask"
                />
            </form>
            <ul>
                <li
                    v-for="(task, index) in tasks"
                    :key="index"
                    class="flex items-center justify-between bg-gray-100 p-2 rounded-lg mb-2"
                >
                    <span
                        :class="{
                            'line-through text-gray-400': task.completed,
                        }"
                    >
                        {{ task.text }}
                    </span>
                    <div class="flex space-x-2">
                        <button
                            @click="toggleTask(index)"
                            class="text-green-500 hover:text-green-700"
                        >
                            ✔
                        </button>
                        <button
                            @click="deleteTask(index)"
                            class="text-red-500 hover:text-red-700"
                        >
                            ✖
                        </button>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

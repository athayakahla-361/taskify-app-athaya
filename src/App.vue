<script setup>

import { ref } from 'vue'

// states: buat menyimpan data tugas tau tasks
const tasks = ref([])

// states: buat menyimpan inputan dari form
const inputTask = ref('')

// action: buat menambahkan tugas baru ke dalam daftar tasks
const addTask = (title) => {

  // bikin object task baru
  const newTask = {
    id: new Date().getTime(),
    title: title,
    status: false
  }

  tasks.value.push(newTask)

  inputTask.value = ''
}

// action: buat menghapus tugas berdasarkan ID
const deleteTask = (id) => {
  
  // cari dulu task berdasarkan ID
  const task = tasks.value.find(item => item.id == id)

  // jika task tidak ditemukan, kita munculkan alert
  if (!task) {
    alert("Task tidak ditemukan!")
    return
  }

  // minta konfirmasi ke user
  const confirmation = confirm("Apakah anda yakin ingin menghapus?")

  if (confirmation) {
     // hapus task dari state tasks
  tasks.value = tasks.value.filter(item => item.id !== id)
  }
}

</script>

<template>
  <!-- Background Utama bertema Palet Warna Blue Bell & Sky Reflection -->
  <div class="palette-bg min-h-screen py-10 flex items-center justify-center font-sans">
    
    <section class="mx-auto max-w-xl px-4 w-full">

      <!-- Main Card Outer Frame -->
      <div class="rounded-[2.5rem] bg-[#4893C6] p-4 sm:p-6 border-4 border-[#2d618a] shadow-[0_10px_0_#2d618a] relative overflow-hidden">
        
        <!-- Awning / Kanopi Tenda Atas -->
        <div class="flex justify-center items-center -mt-4 -mx-6 mb-4 pt-3 pb-2 bg-[#B7D7EA] border-b-4 border-[#2d618a] relative">
          <div class="absolute -top-1 left-0 right-0 flex justify-around opacity-90 pointer-events-none">
            <span class="inline-block w-8 h-4 bg-[#64A4CE] rounded-b-full border-b-2 border-x-2 border-[#2d618a]"></span>
            <span class="inline-block w-8 h-4 bg-[#E2EFF6] rounded-b-full border-b-2 border-x-2 border-[#2d618a]"></span>
            <span class="inline-block w-8 h-4 bg-[#64A4CE] rounded-b-full border-b-2 border-x-2 border-[#2d618a]"></span>
            <span class="inline-block w-8 h-4 bg-[#E2EFF6] rounded-b-full border-b-2 border-x-2 border-[#2d618a]"></span>
            <span class="inline-block w-8 h-4 bg-[#64A4CE] rounded-b-full border-b-2 border-x-2 border-[#2d618a]"></span>
            <span class="inline-block w-8 h-4 bg-[#E2EFF6] rounded-b-full border-b-2 border-x-2 border-[#2d618a]"></span>
          </div>

          <!-- Banner Welcome / Header -->
          <div class="mt-2 bg-[#36739b] text-[#E2EFF6] px-6 py-1.5 rounded-full border-2 border-[#2d618a] shadow-sm text-center">
            <h1 class="text-lg font-bold tracking-wider flex items-center gap-2 justify-center">
              <span>❖</span> Taskify-Vue <span>❖</span>
            </h1>
          </div>
        </div>

        <!-- Inner Content Window -->
        <div class="rounded-2xl bg-[#E2EFF6] p-5 border-2 border-[#2d618a] shadow-inner">
          
          <!-- Subheader / Status Badge -->
          <div class="mb-5 flex flex-wrap items-center justify-between gap-2 border-b-2 border-dashed border-[#8DBEDC] pb-3">
            <div class="flex items-center gap-2 text-xs font-bold text-[#2d618a]">
              <span class="bg-[#64A4CE] text-white px-2.5 py-0.5 rounded-full border border-[#2d618a]">🍧 Daftar Tugas</span>
              <span>Daily Tasks Sheet</span>
            </div>
            <div class="text-[11px] bg-[#B7D7EA] text-[#2d618a] px-3 py-0.5 rounded-full border border-[#8DBEDC] font-semibold">
              Status: Active 🍨
            </div>
          </div>

          <!-- Formulir Tambah Tugas -->
          <form 
            @submit.prevent="addTask(inputTask)"
            action="" 
            class="flex flex-col sm:flex-row gap-3">
            
            <div class="relative flex-1">
              <input
                v-model="inputTask"
                type="text"
                placeholder="Masukkan tugas baru..."
                aria-label="Tugas baru"
                class="w-full rounded-xl border-2 border-[#2d618a] bg-[#FFFFFF] px-4 py-2.5 text-[#2d618a] placeholder-[#8DBEDC] font-medium outline-none focus:ring-2 focus:ring-[#64A4CE] transition shadow-inner"
              />
            </div>

            <button
              type="submit"
              class="rounded-xl bg-[#64A4CE] hover:bg-[#4893C6] border-2 border-[#2d618a] px-6 py-2.5 font-bold text-[#FFFFFF] shadow-[2px_3px_0px_#2d618a] active:translate-y-0.5 active:shadow-none transition flex items-center justify-center gap-1 cursor-pointer"
            >
              <span>+</span> Tambah
            </button> 
          </form>

          <!-- Daftar Tugas -->
          <ul id="task-list" class="mt-5 space-y-3" v-auto-animate>
            <li 
              v-for="task in tasks" 
              :key="task.id" 
              class="flex items-center justify-between rounded-xl bg-[#8DBEDC] border-2 border-[#2d618a] px-4 py-3 shadow-[2px_3px_0px_#2d618a] transition"
            >
              <div class="flex items-center gap-3">
                <input 
                  v-model="task.status"
                  type="checkbox" 
                  class="h-5 w-5 rounded border-2 border-[#2d618a] accent-[#4893C6] cursor-pointer" 
                />
                <span 
                  class="text-[#1A3A52] font-semibold transition-all"
                  :class="task.status ? 'line-through opacity-40' : ''"
                >
                  {{ task.title }}   
                </span>
              </div>  

              <button 
                @click="deleteTask(task.id)" 
                class="text-[#8B0000] hover:text-[#FFFFFF] bg-[#FFD1D1] hover:bg-[#CC4444] border-2 border-[#2d618a] font-bold text-xs px-3 py-1 rounded-lg transition shadow-sm cursor-pointer"
              >
                Hapus
              </button>
            </li>
          </ul>

          <!-- State jika belum ada task -->
          <div v-if="tasks.length === 0" class="mt-5 text-center py-6 border-2 border-dashed border-[#8DBEDC] rounded-xl bg-[#F4F9FC]">
            <p class="text-xs text-[#36739b] font-semibold">Belum ada tugas di menu hari ini. Yuk catat sekarang! ✨</p>
          </div>

        </div>

        <!-- Watermark / Footer Style Carrd -->
        <div class="mt-3 text-center">
          <span class="text-[11px] text-[#B7D7EA] font-medium tracking-wide">
            Vue • Edition 
          </span>
        </div>

      </div>

    </section>
  </div>
</template>

<style scoped>
/* Motif Garis-Garis Diagonal menggunakan palet warna dari gambar */
.palette-bg {
  background-color: #B7D7EA;
  background-image: repeating-linear-gradient(
    45deg,
    #8DBEDC,
    #8DBEDC 15px,
    #B7D7EA 15px,
    #B7D7EA 30px
  );
}
</style>
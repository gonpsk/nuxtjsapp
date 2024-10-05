<template>
  <div class="bg-light min-vh-100">
    <NuxtRouteAnnouncer />

    <!-- เลือกขนาด -->
    <h1 class="py-2 fw-bold fs-4 ms-2">ขนาด</h1>
    <div class="row mt-3 px-4">
      <div class="col-4">
        <a
          href="#"
          class="btn bg-white w-100 mb-2 text-center d-flex align-items-center"
          :class="{ 'bg-light-blue text-white': isActive === 'vertical' }"
          @click.prevent="setSize('vertical')"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="30"
            height="36"
            class="bi bi-square me-2"
            viewBox="0 0 16 16"
          >
            <path
              d="M5 1a1 1 0 0 1 1 1v14a1 1 0 0 1-1 1H1a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h4z"
              fill="white"
              stroke="blue"
              stroke-width="1"
            />
          </svg>
          แนวตั้ง
        </a>
      </div>
      <div class="col-4">
        <a
          href="#"
          class="btn bg-white w-100 mb-2 text-center d-flex align-items-center"
          :class="{ 'bg-light-blue text-white': isActive === 'horizontal' }"
          @click.prevent="setSize('horizontal')"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="70"
            height="30"
            class="bi bi-square me-2"
            viewBox="0 0 16 16"
          >
            <path
              d="M1 5a1 1 0 0 1 1-1h14a1 1 0 0 1 1 1v4a1 1 0 0 1-1 1H2a1 1 0 0 1-1-1V5z"
              fill="white"
              stroke="blue"
              stroke-width="1"
            />
          </svg>
          แนวนอน
        </a>
      </div>
      <div class="col-4">
        <a
          href="#"
          class="btn bg-white w-100 mb-2 text-center d-flex align-items-center"
          :class="{ 'bg-light-blue text-white': isActive === 'square' }"
          @click.prevent="setSize('square')"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="30"
            height="36"
            class="bi bi-square me-2"
            viewBox="0 0 16 16"
          >
            <path
              d="M2 2h12v12H2V2z"
              fill="white"
              stroke="blue"
              stroke-width="1"
            />
          </svg>
          จตุรัส
        </a>
      </div>
    </div>


    <!-- เลือกหมวดหมู่ -->
    <h1 class="mt-4 fw-bold fs-4 ms-2 mb-2">หมวดหมู่</h1>
    <div class="row px-4">
      <div class="col-4 px-4" v-for="category in categories" :key="category">
        <a
          href="#"
          class="btn bg-white w-100 mb-2 text-center d-flex align-items-center justify-content-center mb-2 rounded"
          :class="{
            'bg-light-blue text-white': isActiveCategories.includes(category),
          }"
          @click.prevent="toggleCategory(category)"
        >
          <span v-if="isActiveCategories.includes(category)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="white"
              class="bi bi-check-circle-fill me-2"
              viewBox="0 0 16 16"
              style="color: #80c8ff"
            >
              <path
                d="M16 8a8 8 0 1 1-16 0 8 8 0 0 1 16 0zm-4.5-1.5a.5.5 0 0 0-.7 0L8 10.293 6.207 8.5a.5.5 0 1 0-.707.707l2 2a.5.5 0 0 0 .707 0l5-5a.5.5 0 0 0 0-.707z"
              />
            </svg>
          </span>
          <span>{{ category }}</span>
        </a>
      </div>
    </div>
    
    <!-- สไตล์ภาพ -->
    <h1 class="mt-4 fw-bold fs-4 ms-2 mb-2">สไตล์ภาพ</h1>
    <div class="row">
      <div class="col-12 col-md-4 px-4 mb-4" v-for="(style, index) in stylesToShow" :key="style">
        <div
          class="bg-primary w-100 rounded position-relative overflow-hidden"
          style="height: 350px; cursor: pointer;"
          :style="{
            borderColor: selectedStyles[index] ? 'blue' : 'white',
            borderWidth: '2px',
            borderStyle: 'solid'
          }"
          @click="toggleStyle(index)"
        >
          <img
            src="https://images.unsplash.com/photo-1720048171180-a8178a198fa8?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            alt=""
            class="img-fluid"
            style="height: 100%; width: 100%; object-fit: cover;"
          />
          
          <div
            class="rounded mx-2"
            :style="{
              backgroundColor: selectedStyles[index] ? 'blue' : 'rgba(255, 255, 255, 0.7)',
              color: selectedStyles[index] ? 'white' : 'black',
            }"
            style="position: absolute; bottom: 0; left: 0; right: 0; padding: 5px;"
          >
            <p class="text-center mb-0 fw-bold">{{ style }}</p>
          </div>

          <div
            class="position-absolute"
            v-if="selectedStyles[index]"
            style="
              top: 50%;
              left: 50%;
              width: 40px; 
              height: 40px; 
              background-color: rgba(0, 123, 255, 0.7); 
              border-radius: 50%; 
              display: flex;
              justify-content: center;
              align-items: center;
              transform: translate(-50%, -50%);
            "
          >
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="white" class="bi bi-check-circle" viewBox="0 0 16 16">
              <path d="M16 8a8 8 0 1 1-16 0 8 8 0 0 1 16 0zm-4.5-1.5a.5.5 0 0 0-.7 0L8 10.293 6.207 8.5a.5.5 0 1 0-.707.707l2 2a.5.5 0 0 0 .707 0l5-5a.5.5 0 0 0 0-.707z"/>
            </svg>
          </div>
        </div>
      </div>
    </div>

    <a 
      v-if="hasMoreStyles" 
      href="#" 
      class="text-center mx-auto d-block fs-4 fw-bold" 
      style="width: fit-content; text-decoration: none; color: purple;" 
      @click.prevent="loadMore"
    >
      โหลดเพิ่ม
    </a>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const isActive = ref(null);
const isActiveCategories = ref([]);
const categories = [
  "การงาน",
  "การเงิน",
  "ความรัก",
  "สุขภาพ",
  "ความมั่นใจ",
  "ความสำเร็จ",
  "วาสนา",
  "ศัตรู",
  "ความหวัง",
  "ความสุข",
  "การเรียน",
  "หายนะ",
  "ครอบครัว/ญาติ",
  "โชค",
];

const styles = [
  "Realistic",
  "Cartoon",
  "Digital",
  "Impressionism",
  "Surrealism",
  "Minimalist",
  "Abstract",
  "Classic",
  "Fantasy",
  "Futuristic",
  '3D',
  'Anime',
  "Street",
  "Pixel Art",
  'Vintage',
  'Modern',
  'Romantic',
  'Greek',
  'Sci-fi'
];

const numberOfStylesToShow = ref(12); // จำนวนสไตล์ภาพที่จะแสดงครั้งแรก
const stylesToShow = computed(() => styles.slice(0, numberOfStylesToShow.value));

const hasMoreStyles = computed(() => numberOfStylesToShow.value < styles.length); // ตรวจสอบว่ามีสไตล์เพิ่มเติมหรือไม่

const selectedStyles = ref(Array(styles.length).fill(false)); // สถานะสำหรับการเลือกสไตล์ภาพ

const setSize = (size) => {
  isActive.value = size;
};

const toggleCategory = (category) => {
  if (isActiveCategories.value.includes(category)) {
    isActiveCategories.value = isActiveCategories.value.filter(item => item !== category);
  } else {
    isActiveCategories.value.push(category);
  }
};

const toggleStyle = (index) => {
  selectedStyles.value[index] = !selectedStyles.value[index]; // เปลี่ยนสถานะการเลือกสไตล์
};

const loadMore = () => {
  if (numberOfStylesToShow.value + 7 <= styles.length) {
    numberOfStylesToShow.value += 7; // เพิ่มขึ้น 6 รายการเมื่อโหลดเพิ่ม
  } else {
    numberOfStylesToShow.value = styles.length; // แสดงรายการทั้งหมด
  }
};
</script>

<style scoped>
.bg-light-blue {
  background-color: #80c8ff !important;
}
</style>

<template>
  <div class="form">
    <steps :items="items" :active="activeItem" />
    <button class="form__back-button" v-if="activeItem > 0 && activeItem < 4" @click="back">Назад</button>
    <div v-if="loading" class="form__loader">
      <loader />
    </div>
    <error-info v-else-if="error" />
    <template v-else>
      <!-- Выбор салона -->
      <salons-list v-if="activeItem == 0 && salons" :salons="salons" @selected="salonSelected" />
      <!-- Выбро сотрудника -->
      <workers-list v-if="activeItem == 1 && workersBySelectedSalon" :workers="workersBySelectedSalon" @selected="workerSelected" />
      <!-- Выбор времени -->
      <times-list v-if="activeItem == 2 && timeTable" :times="timeTable" @selected="timeSelected" />
      <!-- Ввод данных клиента -->
      <user-form v-if="activeItem == 3" v-model="user" @selected="completed" />
      <!-- Вывод клиенту сообщения об успешной записи -->
      <success-info v-if="activeItem == 4" :salon="selectedSalon.address" :master="selectedWorker.fio" :time="selectedTime" />
    </template>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  components: {
    Steps: () => import('@/components/steps'),
    Loader: () => import('@/components/loader'),
    SalonsList: () => import('@/components/salons-list'),
    WorkersList: () => import('@/components/workers-list'),
    TimesList: () => import('@/components/times-list'),
    UserForm: () => import('@/components/user-form'),
    SuccessInfo: () => import('@/components/success-info'),
    ErrorInfo: () => import('@/components/error-info')
  },
  data: () => ({
    items: ['Салон', 'Мастер', 'Время', 'Клиент', 'Готово'],
    activeItem: 0,
    loading: true,
    error: false,
    salons: null,
    workers: null,
    timeTable: null,
    selectedSalon: null,
    selectedWorker: null,
    selectedTime: null,
    user: {
      fio: '',
      phone: '+7'
    }
  }),
  computed: {
    workersBySelectedSalon() {
      if (!this.selectedSalon) return this.workers
      return this.workers.filter(worker => worker.idsalon == this.selectedSalon.id)
    }
  },
  methods: {
    back() {
      if (this.activeItem > 0) this.activeItem--
      this.error = false
    },
    async loadSalons() {
      this.loading = true
      try {
        this.salons = (await axios.get('salon.json')).data
      } catch {
        this.error = true
      }
      this.loading = false
    },
    async loadWorkers() {
      this.loading = true
      try {
        this.workers = (await axios.get('workers.json')).data
      } catch {
        this.error = true
      }
      this.loading = false
    },
    async loadTimeTable() {
      this.loading = true
      try {
        this.timeTable = (await axios.get('gettimetable.json')).data
      } catch {
        this.error = true
      }
      this.loading = false
    },
    async singUp() {
      this.loading = true
      try {
        // 404 потому что POST запрос
        // await axios.post('approve.json', {
        //   salonId: this.selectedSalon.id,
        //   workerId: this.selectedWorker.id,
        //   time: this.selectedTime,
        //   fio: this.user.fio,
        //   phone: this.user.phone
        // })

        // Для теста GET запрос
        await axios.get('approve.json', {
          params: {
            salonId: this.selectedSalon.id,
            workerId: this.selectedWorker.id,
            time: this.selectedTime,
            fio: this.user.fio,
            phone: this.user.phone
          }
        })
      } catch {
        this.error = true
      }
      this.loading = false
    },
    async salonSelected(salon) {
      this.selectedSalon = salon
      await this.loadWorkers()
      this.activeItem++
    },
    async workerSelected(worker) {
      this.selectedWorker = worker
      await this.loadTimeTable()
      this.activeItem++
    },
    timeSelected(time) {
      this.selectedTime = time
      this.activeItem++
    },
    async completed() {
      this.activeItem++
      await this.singUp()
    }
  },
  created() {
    this.loadSalons()
  }
}
</script>

<style lang="scss" scoped>
.form {
  height: 500px;
  width: 400px;
  max-width: 95vw;
  background-color: #efeeee;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: -6px -6px 16px #fff, 6px 6px 16px #d1cdc7;
  display: flex;
  flex-direction: column;

  .form__back-button {
    border: none;
    outline: none;
    cursor: pointer;
    background-color: lightyellow;
    padding: 8px;
  }

  .form__loader {
    width: 100%;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>

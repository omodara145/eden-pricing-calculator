<template>
  <div class="ec">
    <div class="ec-body">
      <div class="ec-container">
        <el-row type="flex">
          <el-col :span="24" class="ec-section">
            <h1>Select & Customize Services</h1>
            <div class="ec-pill">
              <span>NGN {{ totalFee }} </span>
            </div>
          </el-col>
        </el-row>
        <el-form label-position="top" :model="form" ref="form">
          <el-row type="flex" :gutter="100">
            <el-col :sm="24" :md="8" class="ec-sub--section">
              <h3>Laundry</h3>
              <div class="ec-form--items">
                <el-form-item label="Quantity (bag)">
                  <el-select v-model="form.laundry.quantity">
                    <el-option label="1" :value="1"></el-option>
                    <el-option label="2" :value="2"></el-option>
                    <el-option label="3" :value="3"></el-option>
                    <el-option label="4" :value="4"></el-option>
                    <el-option label="5" :value="5"></el-option>
                  </el-select>
                  <el-tooltip content="Clear selection" placement="right">
                    <div>
                      <i v-if="form.laundry.quantity !== ''"
                         class="clear-field el-icon-circle-close" @click="form.laundry.quantity = ''"></i>
                    </div>
                  </el-tooltip>
                </el-form-item>
                <el-form-item label="Frequency">
                  <el-select v-model="form.laundry.frequency">
                    <el-option label="Bi-weekly" value="bi_weekly"></el-option>
                    <el-option label="Weekly" value="weekly"></el-option>
                    <el-option label="Monthly" value="monthly"></el-option>
                  </el-select>
                  <el-tooltip content="Clear selection" placement="right">
                    <div>
                      <i v-if="form.laundry.frequency !== ''"
                         class="clear-field el-icon-circle-close" @click="form.laundry.frequency = ''"></i>
                    </div>
                  </el-tooltip>
                </el-form-item>
              </div>
            </el-col>
            <el-col :sm="24" :md="8" class="ec-sub--section">
              <h3>Home Cleaning</h3>
              <div class="ec-form--items">
                <el-form-item label="Bedrooms (to estimate home size)">
                  <el-select v-model="form.cleaning.rooms">
                    <el-option label="1" :value="1"></el-option>
                    <el-option label="2" :value="2"></el-option>
                    <el-option label="3" :value="3"></el-option>
                    <el-option label="4" :value="4"></el-option>
                    <el-option label="5+" :value="5"></el-option>
                  </el-select>
                  <el-tooltip content="Clear selection" placement="right">
                    <div>
                      <i v-if="form.cleaning.rooms !== ''"
                         class="clear-field el-icon-circle-close" @click="form.cleaning.rooms = ''"></i>
                    </div>
                  </el-tooltip>
                </el-form-item>
                <el-form-item label="Frequency">
                  <el-select v-model="form.cleaning.frequency">
                    <el-option label="Bi-weekly" value="bi_weekly"></el-option>
                    <el-option label="Weekly" value="weekly"></el-option>
                    <el-option label="Monthly" value="monthly"></el-option>
                  </el-select>
                  <el-tooltip content="Clear selection" placement="right">
                    <div>
                      <i v-if="form.cleaning.frequency !== ''"
                         class="clear-field el-icon-circle-close" @click="form.cleaning.frequency = ''"></i>
                    </div>
                  </el-tooltip>
                </el-form-item>
              </div>
            </el-col>
            <el-col :sm="24" :md="8" class="ec-sub--section">
              <h3>Meals</h3>
              <el-form-item label="Frequency">
                <el-select v-model="form.meals.frequency">
                  <el-option label="Daily" value="daily"></el-option>
                  <el-option label="Bi-weekly" value="bi_weekly"></el-option>
                  <el-option label="Weekly" value="weekly"></el-option>
                </el-select>
                <el-tooltip content="Clear selection" placement="right">
                  <div>
                    <i v-if="form.meals.frequency !== ''"
                       class="clear-field el-icon-circle-close" @click="form.meals.frequency = ''"></i>
                  </div>
                </el-tooltip>
              </el-form-item>
            </el-col>
          </el-row>
        </el-form>
      </div>
    </div>
    <div class="ec-footer">
      <div class="ec-container">
        <el-button type="primary" class="ec-web--button">Get Started<i class="el-icon-arrow-right"></i></el-button>
        <el-button type="primary" class="ec-mobile--button">Pay NGN {{ totalFee }}</el-button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data() {
      return {
        totalFee: 0,
        meals: {
          daily: 86000,
          bi_weekly: 28234,
          weekly: 48200
        },
        laundry: {
          bi_weekly: 23000,
          weekly: 35000,
          monthly: 12967
        },
        cleaning: {
          bi_weekly: 19000,
          weekly: 27000,
          monthly: 10967
        },
        form: {
          laundry: {
            quantity: "",
            frequency: ""
          },
          cleaning: {
            rooms: "",
            frequency: ""
          },
          meals: {
            frequency: ""
          }
        }
      }
    },
    watch: {
      form: {
        handler() {
          this.calculateFee();
        },
        deep: true
      }
    },
    methods: {
      calculateLaundry() {
        let laundryFreq = this.form.laundry.frequency;
        let laundryQuantity = this.form.laundry.quantity;
        return (this.laundry[laundryFreq] * laundryQuantity) || 0;
      },
      calculateCleaning() {
        let cleaningFreq = this.form.cleaning.frequency;
        let cleaningRooms = this.form.cleaning.rooms;
        let total;

        if (cleaningFreq) {
          switch (cleaningFreq) {
            case "weekly":
              if (cleaningRooms === 3 || cleaningRooms === 4) {
                total = this.cleaning[cleaningFreq] + 4000
              } else if (cleaningRooms === 5) {
                total = this.cleaning[cleaningFreq] + 8000
              } else {
                total = this.cleaning[cleaningFreq]
              }
              break;
            case "bi_weekly":
              if (cleaningRooms === 3 || cleaningRooms === 4) {
                total = this.cleaning[cleaningFreq] + 2000
              } else if (cleaningRooms === 5) {
                total = this.cleaning[cleaningFreq] + 4000
              } else {
                total = this.cleaning[cleaningFreq]
              }
              break;
            case "monthly":
              if (cleaningRooms === 3 || cleaningRooms === 4) {
                total = this.cleaning[cleaningFreq] + 1000
              } else if (cleaningRooms === 5) {
                total = this.cleaning[cleaningFreq] + 2000
              } else {
                total = this.cleaning[cleaningFreq]
              }
              break;
            default:
              return total;
          }
        } else {
          total = 0;
        }

        return total;

      },
      calculateMeals() {
        let mealFreq = this.form.meals.frequency;
        return this.meals[mealFreq] || 0;
      },
      calculateFee() {
        let cleaning = this.calculateCleaning();
        let laundry = this.calculateLaundry();
        let meals = this.calculateMeals();
        this.totalFee =  laundry + cleaning + meals
      },
      showS() {
        console.log(event)
      }
    }
  }
</script>

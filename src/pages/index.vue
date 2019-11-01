<template>
  <div class="ec">
    <div class="ec-body">
      <div class="ec-container">
        <el-row type="flex">
          <el-col :span="24" class="ec-section">
            <h1>Select & Customize Services</h1>
            <div class="ec-pill">
              <span>NGN {{ totalFee }}</span>
            </div>
          </el-col>
        </el-row>
        <el-form label-position="top">
          <el-row type="flex" :gutter="100">
            <el-col :md="8" class="ec-sub--section">
              <h3>Laundry</h3>
              <el-form-item label="Quantity (bag)">
                <el-select v-model="form.laundry.quantity" placeholder="">
                  <el-option label="1" value="1"></el-option>
                  <el-option label="2" value="2"></el-option>
                  <el-option label="3" value="3"></el-option>
                  <el-option label="4" value="4"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="Frequency">
                <el-select v-model="form.laundry.frequency" placeholder="">
                  <el-option label="Daily" value="daily"></el-option>
                  <el-option label="Bi-weekly" value="bi-weekly"></el-option>
                  <el-option label="Weekly" value="weekly"></el-option>
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :md="8" class="ec-sub--section">
              <h3>Home Cleaning</h3>
              <el-form-item label="Bedrooms (to estimate home size)">
                <el-select v-model="form.homeCleaning.quantity" placeholder="">
                  <el-option label="1" value="1"></el-option>
                  <el-option label="2" value="2"></el-option>
                  <el-option label="3" value="3"></el-option>
                  <el-option label="4" value="4"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="Frequency">
                <el-select v-model="form.laundry.frequency" placeholder="">
                  <el-option label="Bi-weekly" value="bi-weekly"></el-option>
                  <el-option label="Weekly" value="weekly"></el-option>
                  <el-option label="Monthly" value="monthly"></el-option>
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :md="8" class="ec-sub--section">
              <h3>Meals</h3>
              <el-form-item label="Frequency">
                <el-select v-model="form.laundry.frequency" placeholder="">
                  <el-option label="Daily" value="daily"></el-option>
                  <el-option label="Bi-weekly" value="bi-weekly"></el-option>
                  <el-option label="Weekly" value="weekly"></el-option>
                </el-select>
              </el-form-item>
            </el-col>
          </el-row>
        </el-form>
      </div>
    </div>
    <div class="ec-footer">
      <div class="ec-container">
        <el-button type="primary">Get Started<i class="el-icon-arrow-right"></i></el-button>
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
        options: ["Daily", "Bi-weekly", "Weekly"],
        form: {
          laundry: {
            quantity: "",
            frequency: ""
          },
          homeCleaning: {
            quantity: "",
            frequency: ""
          },
          meals: {
            quantity: "",
            frequency: ""
          }
        }
      }
    }
  }
</script>

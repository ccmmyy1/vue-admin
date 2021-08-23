<template>
  <div class="container">
    <div class="form-box">
      <el-form ref="form"
               v-model="form"
               label-width="80px">
        <el-form-item label="姓名">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="学历">
          <el-select v-model="form.school"
                     placeholder="请选择">
            <el-option key="1"
                       label="本科"
                       value="1"></el-option>
            <el-option key="2"
                       label="硕士"
                       value="2"></el-option>
            <el-option key="3"
                       label="博士"
                       value="3"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="日期">
          <el-col :span="11">
            <el-date-picker type="datetime"
                            v-model="form.startDate"
                            placeholder="请选择开始日期"
                            value-format="yyyy-MM-dd HH:mm:ss">
            </el-date-picker>
          </el-col>
          <el-col class="line"
                  :span="2">-</el-col>
          <el-col :span="11">
            <el-date-picker type="datetime"
                            v-model="form.endDate"
                            placeholder="请选择结束日期"
                            value-format="yyyy-MM-dd HH:mm:ss">
            </el-date-picker>
          </el-col>
        </el-form-item>
        <el-form-item label="城市">
          <el-cascader :options="options"
                       v-model="form.options"></el-cascader>
        </el-form-item>
        <el-form-item label="选择开关">
          <el-switch v-model="form.delivery"></el-switch>
        </el-form-item>
        <el-form-item label="单选框">
          <el-radio-group v-model="form.gender">
            <el-radio label="男生"></el-radio>
            <el-radio label="女生"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="爱好">
          <el-checkbox-group v-model="form.type">
            <el-checkbox label="羽毛球"
                         name="type"></el-checkbox>
            <el-checkbox label="跑步"
                         name="type"></el-checkbox>
            <el-checkbox label="摄影"
                         name="type"></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-form-item label="文本框">
          <el-input type="textarea"
                    row="5"
                    v-model="form.desc"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary"
                     @click="onSubmit">提交</el-button>
          <el-button>取消</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
import cityData from '../../utils/cityData';
// json数据text换成label
const sortCityList = []
for (let i in cityData) {
  let city = {}
  city.value = cityData[i].value
  city.label = cityData[i].text
  city.children = cityData[i].children
  for (let j in city.children) {
    // eslint-disable-next-line no-self-assign
    city.children[j].value = city.children[j].value
    city.children[j].label = city.children[j].text
    // eslint-disable-next-line no-self-assign
    city.children[j].children = city.children[j].children
    for (let k in city.children[j].children) {
      // eslint-disable-next-line no-self-assign
      city.children[j].children[k].value = city.children[j].children[k].value
      city.children[j].children[k].label = city.children[j].children[k].text
    }
  }
  sortCityList.push(city);
}
export default {
  data () {
    return {
      options: sortCityList,
      form: {
        name: '',
        school: '',
        startDate: '',
        endDate: '',
        delivery: true,
        gender: '男生',
        type: ['摄影'],
        desc: '',
        options: []
      }
    }
  },
  methods: {
    onSubmit () {
      console.log('提交成功！', this.form);
      this.$message.success('提交成功！');
    }

  }

}
</script>

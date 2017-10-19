<template>
  <doc-section id="datepicker" name="Datepicker">
    <div class="bs-example">
      <p>
        <pre>Selected date is: {{dateString}}</pre>
      </p>
      <datepicker :min-date="minimumDate" :max-date="maxDate" ref="dp" v-model="date" :name="name" :disabled-days-of-week="disabled" :format="format" :clear-button="clear" :placeholder="placeholder" width="370px"></datepicker>
      <h4>Disabled days of week</h4>

      <v-select multiple v-model="disabled" :options="[0,1,2,3,4,5,6]"></v-select>

      <h4>Format</h4>
      <v-select v-model="format" :options="formats"></v-select>

      <h4>Minimum Date</h4>
      <datepicker ref="dp" v-model="minDate" :name="name" :format="format" :clear-button="true" placeholder="Minimum Date" width="370px"></datepicker>
      
      <h4>Maximum Date</h4>
      <datepicker :min-date="minimumDate" ref="dp" v-model="maxDate" :name="name" :format="format" :clear-button="true" placeholder="Maximum Date" width="370px"></datepicker>

      <h4>Reset button</h4>
      <checkbox :value="clear" @checked="clear = arguments[0]" type="primary">toggle clear button</checkbox>
    </div>
    <doc-code language="markup">
      &lt;datepicker
      &emsp;&emsp;v-model="value"
      &emsp;&emsp;:disabled-days-of-Week="disabled"
      &emsp;&emsp;:format="format"
      &emsp;&emsp;:clear-button="clear"
      &emsp;&emsp;:min-date="minDate"
      &emsp;&emsp;:max-date="maxDate"
      &emsp;&emsp;:placeholder="placeholder">
      &lt;/datepicker>
    </doc-code>
    <doc-table>
      <div>
        <p>clear-button</p>
        <p><code>Boolean</code></p>
        <p>false</p>
        <p>If <strong>true</strong> shows an &times; shaped button to clear the selected date.
          Usefull in forms where date entry is optional.</p>
      </div>
      <div>
        <p>disabled-days-of-week</p>
        <p><code>Array</code></p>
        <p></p>
        <p>Days of the week that should be disabled. Values are 0 (Sunday) to 6 (Saturday).
           Multiple values should be comma-separated.</p>
      </div>
      <div>
        <p>format</p>
        <p><code>String</code></p>
        <p><code>MMMM/dd/yyyy</code></p>
        <p>The date format, combination of d, dd, M, MM, MMM, MMMM, yyyy.</p>
      </div>
      <div>
        <p>min-date</p>
        <p><code>String</code></p>
        <p></p>
        <p>Defines the minimum available date. E.g. "2017-10-19"</p>
      </div>
      <div>
        <p>max-date</p>
        <p><code>String</code></p>
        <p></p>
        <p>Defines the maximum available date. E.g. "2017-10-19"</p>
      </div>
      <div>
        <p>name</p>
        <p><code>String</code></p>
        <p></p>
        <p>Name to put on the input field</p>
      </div>
      <div>
        <p>placeholder</p>
        <p><code>String</code></p>
        <p></p>
        <p>Placeholder to put on the input field when no date (null or empty) is set</p>
      </div>
      <div>
        <p>value</p>
        <p><code>String</code></p>
        <p></p>
        <p>Value of the input DOM</p>
      </div>
      <div>
        <p>width</p>
        <p><code>String</code></p>
        <p></p>
        <p>Width of the input DOM</p>
      </div>
      <div>
        <p>icons-font</p>
        <p><code>String</code></p>
        <p><code>glyphicon</code></p>
        <p>The icon font used for arrows. Can be 'glyphicon' or 'fa' (Font Awesome)</p>
      </div>
    </doc-table>
    <doc-table type="Events">
      <div>
        <p>input</p>
        <p>(<code>value:string</code>)</p>
        <p>Return the selected value.</p>
      </div>
    </doc-table>
  </doc-section>
</template>

<script>
import docSection from './utils/docSection.vue'
import docTable from './utils/docTable.js'
import docCode from './utils/docCode.js'
import Checkbox from 'src/Checkbox.vue'
import Datepicker from 'src/Datepicker.vue'
import vSelect from 'src/Select.vue'
import vOption from 'src/Option.vue'

const currentDate = new Date();
const currentDateString = `${currentDate.getFullYear()}-${currentDate.getMonth() + 1}-${currentDate.getDate()}`

export default {
  components: {
    docSection,
    docTable,
    docCode,
    Checkbox,
    Datepicker,
    vSelect,
    vOption
  },
  data () {
    return {
      clear: true,
      disabled: [],
      format: 'yyyy-MM-dd',
      formats: ['dd/MM/yyyy', 'dd-MM-yyyy', 'yyyy,MM,dd', 'yyyy-MM-dd', 'yyyy.MM.dd', 'MMM/dd/yyyy', 'MMMM/dd/yyyy', 'MM/dd/yyyy', 'MM-dd-yyyy'],
      placeholder: 'placeholder is displayed when value is null or empty',
      date: currentDateString ,
      minDate: '',
      maxDate: ''
    }
  },
  computed: {
    dateString () {
      let date
      if (this.date.length === 10 && (this.format === 'dd-MM-yyyy' || this.format === 'dd/MM/yyyy')) {
        date = new Date(this.date.substring(6, 10), this.date.substring(3, 5), this.date.substring(0, 2))
      } else {
        date = new Date(this.date)
      }
      return isNaN(date.getFullYear()) ? new Date().toString() : date.toString()
    },
    minimumDate () {
      return this.minDate != '' ? this.minDate : null;
    },
    maximumDate () {
      return this.maxDate != '' ? this.maxDate : null;
    }
  },
}
</script>

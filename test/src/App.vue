<template>
  <header>
  </header>

  <main>
    <div class="form-container bg=white-100" >
            <h1>Registration Form</h1>
            <form @submit.prevent="handleSubmit" class="p-2">
                <Selector v-model="selectedValue" label="Выберите значение" :values="customValues"/>
                <Input
                    placeholder="Enter your username"
                />  
                <TextArea
                    placeholder="Enter your email"
                />
                
                <p>Selected value: {{ selectedValue }}</p>
                <button type="submit">Submit</button>
            </form>
        </div>
  </main>
</template>
<script>
    import { ref } from 'vue';
    import Input from './components/Input.vue';
    import TextArea from './components/TextArea.vue';
    import Selector from './components/Selector.vue';


    export default {
        components: {
            Selector,
            Input,
            TextArea
        },
        setup() {
            
            const selectedValue = ref('');
            const customValues = ref(["Нет опыта", "От 1 года до 3 лет", "От 3 до 6 лет", "Больше 6"]);

            return {
                selectedValue,
                customValues
            };
        }
    };
</script>

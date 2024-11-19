<script setup>
(() => {
    const dynamicSelect = (id1, id2) => {
      // Определение переменных, ссылающихся на списки
      const sel1 = document.getElementById(id1);
      const sel2 = document.getElementById(id2);
      // Клонирование динамического списка
      const clone = sel2.cloneNode(true);
      // Определение переменных для клонированных элементов списка
      const clonedOptions = clone.getElementsByTagName("option");
      // Вызов функции собирающей вызываемый список
      refreshDynamicSelectOptions(sel1, sel2, clonedOptions);
      // При изменении выбранного элемента в первом списке: // вызов функции пересобирающей вызываемый список
      sel1.addEventListener('change', () => {
        refreshDynamicSelectOptions(sel1, sel2, clonedOptions);
      });
    };
  
    // Функция для сборки динамического списка
    const refreshDynamicSelectOptions = (sel1, sel2, clonedOptions) => {
      // Удаление всех элементов динамического списка
      while (sel2.options.length) {
        sel2.remove(0);
      }
      const selectedOption = sel1.options[sel1.selectedIndex].value;
      // Перебор клонированных элементов списка
      for (let i = 0; i < clonedOptions.length; i++) {
        const option = clonedOptions[i];
        // Если название класса клонированного option эквивалентно "select"
        // либо эквивалентно значению option первого списка
        if (option.classList.contains('select') ||
          option.classList.contains(selectedOption)) {
          // его нужно клонировать в динамически создаваемый список
          sel2.appendChild(option.cloneNode(true));
        }
      }
      // Отправляем событие change выбранного select
      const event = document.createEvent('HTMLEvents');
      event.initEvent('change', true, false);
      sel2.dispatchEvent(event);
    };
  
    // Вызов скрипта при загрузке страницы
    document.addEventListener("DOMContentLoaded", () => {
      dynamicSelect("select-1", "select-2");
      dynamicSelect("select-2", "select-3");
    });
  })();
</script>

<template>
  <form action="#" method="post">
        <select id="select-1">
          <option value="select">Select...</option>
          <option value="a">Bryansk</option>
          <option value="b">Moskow</option>
          <option value="c">Caluga</option>
        </select>
        
        <select id="select-2">
          <option class="select" value="select">Select...</option>
          <option class="a" value="aa">Ceh1</option>
          <option class="a" value="ab">Ceh2</option>
          <option class="b" value="ba">Ceh1</option>
          <option class="c" value="ca">Ceh3</option>
        </select>
        
        <select id="select-3">
          <option class="select" value="select">Select...</option>
          <option class="aa" value="aaa">Ivanow</option>
          <option class="aa" value="aab">Petrow</option>
          <option class="ab" value="aba">Sidorow</option>
          <option class="ab" value="abb">Evgeniev</option>   
          <option class="ba" value="baa">Gidov</option>
          <option class="ba" value="bab">Fedorov</option>
          <option class="ca" value="caa">C-A-A</option>
          <option class="ca" value="cab">Mishin</option>
        </select>
        </form>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

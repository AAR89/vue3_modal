# vue3_modal

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

Прямая ссылка на gh-pages: https://aar89.github.io/vue3_modal/

Цель:
Разработать Vue 3 компонент с использованием TypeScript и Composition API, реализующий функционал модального окна с деревом папок.

Задание:

1. Создать новый Vue-проект с использованием Vue 3, TypeScript и Composition API. Можно использовать официальные инструменты (create-vue) или аналогичные.
2. Реализовать базовый компонент, который включает:
   Кнопку с текстом «Открыть» на странице.
   При нажатии на кнопку открывается модальное окно с деревом папок.
3. Модальное окно с деревом папок:
   Использует отдельный компонент для модального окна.
   Включает функционал:
   3.1) Текст заголовка модального окна, передаваемый как пропс.
   3.2) Дерево папок, которое:
   3.2.1) Построено на основе mock-данных.
   3.2.2) Поддерживает раскрытие/закрытие узлов дерева (глубина вложенности не ограничена).
   3.2.3) Позволяет выделить одну папку.
   3.3) Кнопку «Ок», которая:
   3.3.1) Закрывает модальное окно.
   3.3.2) Генерирует кастомное событие select, передающее идентификатор выбранной папки.
   3.4) Кнопку «Закрыть», которая закрывает модальное окно без дополнительных действий.
4. Mock-данные для дерева папок:
   Пример структуры:
   const mockFolders = [
   { id: 1, name: 'Папка 1', children: [
   { id: 2, name: 'Папка 1.1', children: [] },
   { id: 3, name: 'Папка 1.2', children: [
   { id: 4, name: 'Папка 1.2.1', children: [] }
   ]}
   ]},
   { id: 5, name: 'Папка 2', children: [] },
   ];
5. Компоненты должны быть типизированы с использованием TypeScript.
6. Верстка и стилизация — минимальные, чтобы подчеркнуть функциональность.

Условия выполнения:

1. Код должен быть написан на Vue 3 с использованием Composition API и TypeScript.
2. Все функциональные элементы (модальное окно, дерево папок) должны быть компонентами с четким разделением логики.
3. Взаимодействие между компонентами осуществляется через пропсы и кастомные события.
4. Приложение должно корректно запускаться после выполнения команды npm run serve.

Результат выполнения:

1. Репозиторий (например, на GitHub) с исходным кодом.
2. Инструкция по запуску проекта (если используется что-то помимо стандартного Vue CLI).

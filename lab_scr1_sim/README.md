# Лабораторная работа №2 — вариант 6

## Цель работы

Ознакомиться с настройкой архитектуры процессорного ядра SCR1,
обработкой исключений и работой тестового окружения.

## Задание

Обработать исключение Environment call from M-mode в тесте
`isa/rv32mi/scall.S`. При возникновении исключения вывести сообщение
`envcall`.

## Настройки процессора

- Reset Vector: `0xB000`
- Trap Vector: `0xA880`
- Тест: `isa/rv32mi/scall.S`
- Симулятор: Verilator 5.052

## Выполненные изменения

1. В `src/includes/scr1_arch_description.svh` изменены Reset Vector
   и Trap Vector.
2. В `sim/tests/riscv_isa/rv32_tests.inc` оставлен только тест
   `isa/rv32mi/scall.S`.
3. В `sim/tests/common/link.ld` настроено размещение кода с учётом
   новых адресов.
4. В `sim/tests/common/riscv_macros.h` добавлена обработка
   Environment call from M-mode с выводом сообщения `envcall`.

## Сборка и запуск

Использовалась команда:

`make run_verilator_wf TARGETS="riscv_isa" TRACE=1 CROSS_PREFIX=/usr/bin/riscv64-unknown-elf-`

## Результаты

Тест `scall.hex` завершился успешно.

Сообщение симуляции: `envcallTest passed`.

Итог: `1/1 tests passed`.

В трассе подтверждены адрес сброса `0xB000`, адрес обработчика
`0xA880` и значение `mcause = 0x0000000B`.

## Сохранённые результаты

В каталоге `results` сохранены результат теста, дамп программы,
осциллограмма и общий журнал трассировки SCR1.

Отдельные файлы трассировки MPRF и CSR сформированы фильтрацией
общего журнала `tracelog_core_0.log`.

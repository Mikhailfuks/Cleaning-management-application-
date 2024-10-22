using System;
using System.Collections.Generic;

namespace CleaningApp
{
    // Класс для представления задачи по уборке
    public class CleaningTask
    {
        public int Id { get; set; }
        public string Description { get; set; }
        public bool IsCompleted { get; set; }
        public DateTime DueDate { get; set; }

        // Конструктор
        public CleaningTask(int id, string description, bool isCompleted, DateTime dueDate)
        {
            Id = id;
            Description = description;
            IsCompleted = isCompleted;
            DueDate = dueDate;
        }
    }

    // Класс для управления списком задач по уборке
    public class CleaningManager
    {
        private List<CleaningTask> tasks = new List<CleaningTask>();
        private int nextTaskId = 1;

        // Добавление задачи
        public void AddTask(string description, DateTime dueDate)
        {
            CleaningTask task = new CleaningTask(nextTaskId++, description, false, dueDate);
            tasks.Add(task);
        }

        // Получение списка задач
        public List<CleaningTask> GetTasks()
        {
            return tasks;
        }

        // Отметка задачи как выполненной
        public void MarkTaskCompleted(int id)
        {
            CleaningTask task = tasks.Find(t => t.Id == id);
            if (task != null)
            {
                task.IsCompleted = true;
            }
        }

        // Удаление задачи
        public void RemoveTask(int id)
        {
            tasks.RemoveAll(t => t.Id == id);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Создание менеджера задач по уборке
            CleaningManager cleaningManager = new CleaningManager();

            // Добавление задач
            cleaningManager.AddTask("Пропылесосить", DateTime.Now.AddDays(1));
            cleaningManager.AddTask("Помыть посуду", DateTime.Now.AddHours(2));
            cleaningManager.AddTask("Вынести мусор", DateTime.Now.AddDays(2));

            // Вывод списка задач
            Console.WriteLine("Список задач по уборке:");
            foreach (CleaningTask task in cleaningManager.GetTasks())
            {
                Console.WriteLine($"{task.Id}. {task.Description} (Срок: {task.DueDate:dd.MM.yyyy HH:mm}) {(task.IsCompleted ? "(Выполнено)" : "")}");
            }

            // Отметка задачи как выполненной
            cleaningManager.MarkTaskCompleted(1);
            Console.WriteLine("\nЗадача с Id 1 отмечена как выполненная.");

            // Удаление задачи
            cleaningManager.RemoveTask(2);
            Console.WriteLine("\nЗадача с Id 2 удалена.");

            // Вывод обновленного списка задач
            Console.WriteLine("\nОбновленный список задач:");
            foreach (CleaningTask task in cleaningManager.GetTasks())
            {
                Console.WriteLine($"{task.Id}. {task.Description} (Срок: {task.DueDate:dd.MM.yyyy HH:mm}) {(task.IsCompleted ? "(Выполнено)" : "")}");
            }

            Console.ReadKey();
        }
    }
}

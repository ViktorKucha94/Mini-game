// Конструктор для создания объекта мяча
function Ball(x, y, radius, color) {
  // Свойства мяча: координаты центра, радиус, цвет, скорость по осям x и y
  this.x = x;
  this.y = y;
  this.radius = radius;
  this.color = color;
  this.dx = 2; // Скорость по оси x
  this.dy = -2; // Скорость по оси y

  // Метод для отрисовки мяча на холсте
  this.draw = function() {
    // Сохраняем текущее состояние контекста
    ctx.save();
    // Задаем цвет заливки
    ctx.fillStyle = this.color;
    // Начинаем новый путь
    ctx.beginPath();
    // Рисуем окружность с заданными параметрами
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    // Заканчиваем путь
    ctx.closePath();
    // Заливаем путь цветом
    ctx.fill();
    // Восстанавливаем предыдущее состояние контекста
    ctx.restore();
  };

  // Метод для обновления положения мяча
  this.update = function() {
    // Прибавляем скорость к координатам мяча
    this.x += this.dx;
    this.y += this.dy;

    // Проверяем столкновение с границами холста
    if (this.x + this.radius > canvas.width || this.x - this.radius < 0) {
      // Отражаем мяч по оси x
      this.dx = -this.dx;
    }
    if (this.y - this.radius < 0) {
      // Отражаем мяч по оси y
      this.dy = -this.dy;
    }
    if (this.y + this.radius > canvas.height) {
      // Завершаем игру, если мяч упал за нижнюю границу
      gameOver();
    }
  };
}

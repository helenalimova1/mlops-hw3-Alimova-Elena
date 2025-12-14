Этот сервис предоставляет gRPC-сервер для выполнения предсказаний с использованием модели машинного обучения. Он включает два основных элемента:

• /health: проверка работоспособности сервиса и версии модели.
• /predict: выполнение предсказаний на основе входных данных.

Установите следующие переменные окружения:
• PORT=50051: порт gRPC-сервера.
• MODEL_PATH=/app/models/model.pkl: путь к файлу модели.
• MODEL_VERSION=v1.0.0: версия модели.

▎Инструкции по сборке и запуску

   
1. Установка зависимостей и вызов модели:

   pip install -r requirements.txt --no-input
   python -m grpc_tools.protoc -I./protos --python_out=./protos --grpc_python_out=./protos ./protos/model.proto
   
2. Сборка Docker:

   docker build -t grpc-ml-service .
   
3. Запуск Docker:
   docker run -p 50051:50051 grpc-ml-service
   
Для проверки работоспособности сервиса выполните:
grpcurl -plaintext -proto protos/model.proto localhost:50051 mlservice.v1.PredictionService.Health
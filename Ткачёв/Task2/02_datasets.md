# Данные для ноутбуков

Сами датасеты в репозиторий не положены — CIFAR-10 и GTSRB в сумме тянут на несколько гигабайт,
и гонять такое через git смысла нет. Ниже — откуда их взять и куда положить, чтобы ноутбуки
заработали без правок путей.

## CIFAR-10

Используется `torchvision.datasets.CIFAR10` с `download=False` — ноутбук ожидает, что архив уже
лежит локально.

- Официальный источник: https://www.cs.toronto.edu/~kriz/cifar.html (python-версия, `cifar-10-python.tar.gz`)
- Либо можно один раз вызвать `torchvision.datasets.CIFAR10(root="./CIFAR10", download=True)` —
  `torchvision` сам скачает и распакует архив в указанную папку, если есть доступ в сеть.

Ожидаемый путь в ноутбуках — папка `CIFAR10` рядом с ноутбуком (`root="./CIFAR10"`). `torchvision`
сам разберется со структурой внутри, это стандартный формат от `torchvision.datasets.CIFAR10`.

## GTSRB (German Traffic Sign Recognition Benchmark)

Через `torchvision.datasets.GTSRB` датасет не берется (я очень долго пытался) — сервер с оригинальными архивами
(`sid.erda.dk`) не отдает файлы из-под части сетей. Вместо этого используется зеркало с Kaggle:

- https://www.kaggle.com/datasets/meowmeowmeowmeowmeow/gtsrb-german-traffic-sign

Нужно скачать его (кнопка Download на странице датасета, или `kaggle datasets download -d
meowmeowmeowmeowmeow/gtsrb-german-traffic-sign`, если настроен Kaggle CLI) и распаковать так, чтобы
получилась структура:

```
GTSRB/
├── Train/
│   ├── 0/
│   │   ├── 00000_00000_00000.png
│   │   └── ...
│   ├── 1/
│   ├── ...
│   └── 42/
├── Test/
│   ├── 00000.png
│   └── ...
└── Test.csv
```

В ноутбуках путь к этой папке прописан так — `gtsrb_root = r"D:\coding\Studying\CV\Task2\GTSRB"`.

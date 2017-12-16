# 📦 Упаковщики

В Parcel `Упаковщик` объединяет несколько `Ассетов` вместе в конечный выходной пакет. Это происходит в основном процессе после того, как все ассеты обработаны и создано дерево бандлов. Упаковщики регистрируются на основе типа выходного файла, а ассеты, которые сгенерировали этот тип вывода, отправляются этому пакету для создания окончательного выходного файла.

## Интерфейс упаковщика

```javascript
const {Packager} = require('parcel-bundler');

class MyPackager extends Packager {
  async start() {
    // (опционально) запишите заголовок файла, если это необходимо.
    await this.dest.write(header);
  }

  async addAsset(asset) {
    // запишите ассет в выходной файл.
    await this.dest.write(asset.generated.foo);
  }

  async end() {
    // (опционально) при необходимости напишите файл трейлера.
    await this.dest.end(trailer);
  }
}
```

## Регистрация упаковщика

Вы можете зарегистрировать упаковщик с помощью метода `addPackager`. Он принимает тип файла для регистрации и путь к вашему модулю упаковщика.

```javascript
const Bundler = require('parcel-bundler');

let bundler = new Bundler('input.js');
bundler.addPackager('foo', require.resolve('./MyPackager'));
```

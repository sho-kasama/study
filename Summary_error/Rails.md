

### デフォルトのテンプレートをERBからslimに変更する

config/application.rb
```
class Application < Rails::Application
  config.generators.template_engine = :slim
end
```

### Railsの日本語対応

- [ ] <a href="https://qiita.com/shizuma/items/a52fd0ef5b60d61fa330">Railsの日本語対応</a>
- [ ] <a href="https://qiita.com/MasatoYoshioka@github/items/8d910e793e7c485403bb">rails devise　日本語対応</a>

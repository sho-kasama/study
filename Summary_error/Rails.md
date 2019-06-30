

### デフォルトのテンプレートをERBからslimに変更する

config/application.rb
```
class Application < Rails::Application
  config.generators.template_engine = :slim
end
```


# AI Provider for OpenAI

A PHP integration that connects OpenAI models with the [WordPress PHP AI Client SDK](https://github.com/WordPress/php-ai-client). It can be installed as a Composer package or used as a WordPress plugin.

## Requirements

- PHP 7.4 or higher.
- WordPress 7.0 or higher when used as a WordPress plugin.
- For older WordPress versions, the `wordpress/php-ai-client` package must be installed separately.

## Installation

### Using Composer

Install the package with Composer:

```bash
composer require wordpress/ai-provider-for-openai
```

### As a WordPress Plugin

1. Download the plugin files.
2. Upload them to `/wp-content/plugins/ai-provider-for-openai/`.
3. Ensure the PHP AI Client is installed and activated.
4. Activate the plugin through the WordPress admin dashboard.

## Configuration

The provider authenticates with the OpenAI API using the `OPENAI_API_KEY` environment variable.

Set your API key in your environment or configure it in PHP:

```php
putenv('OPENAI_API_KEY=your-api-key');
```

Keep your API key private. Do not commit real API keys to your repository.

## Usage

### With WordPress

When activated, the provider registers itself with the PHP AI Client during the WordPress `init` hook.

Once both components are configured, you can generate text:

```php
use WordPress\AiClient\AiClient;

$result = AiClient::prompt('Hello, world!')
    ->usingProvider('openai')
    ->generateTextResult();
```

### As a Standalone Package

Register the OpenAI provider with the PHP AI Client registry:

```php
use WordPress\AiClient\AiClient;
use WordPress\OpenAiAiProvider\Provider\OpenAiProvider;

$registry = AiClient::defaultRegistry();
$registry->registerProvider(OpenAiProvider::class);

$result = AiClient::prompt('Explain quantum computing')
    ->usingProvider('openai')
    ->generateTextResult();

echo $result->toText();
```

Ensure the required PHP AI Client packages are installed and your API key is configured before making requests.

## Supported Models

The provider discovers available models through the OpenAI API. Supported capabilities include:

- Text generation with GPT models.
- Image generation with compatible image models.
- Text-to-speech using supported audio models.

Available models and capabilities may change. Refer to the [OpenAI Models documentation](https://platform.openai.com/docs/models) for current information.

## Resources

- [WordPress PHP AI Client](https://github.com/WordPress/php-ai-client)
- [OpenAI API Documentation](https://platform.openai.com/docs/)
- [OpenAI Models](https://platform.openai.com/docs/models)

## License

Refer to the original project's repository for its license and attribution requirements. If redistributing or modifying this project, preserve the applicable license and copyright notices.

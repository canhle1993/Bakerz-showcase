# Deployment And Tech Notes

## Runtime

- PHP 8.2
- Laravel 11
- MySQL / MariaDB
- Apache or Nginx

## Frontend

- Blade templates
- Bootstrap
- jQuery
- Vite for asset workflow

## Integrations

- Google Maps or iframe embed
- Power BI embed
- VNPay

## CI/CD

- GitHub Actions is used for deployment automation
- The current workflow runs on push to the `master` branch
- Deployment is performed over SSH to the online server
- After pulling the latest code, Laravel cache and configuration are cleared as part of the deployment flow

## Deployment Reminder

- Keep the real `.env` private
- Do not upload secrets to the showcase repository
- Use screenshots and diagrams instead of source code

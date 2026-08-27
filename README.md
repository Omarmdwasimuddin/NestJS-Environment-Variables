# Environment Variables

### install @nestjs/config
```bash
npm i @nestjs/config
```
---


> root e .env file toiri koro
### `.env`
```bash
DATABASE_URL=mongodb://localhost:500/mongodb
JWT_SECRET=1234567
```
---


>Module e import koro- ConfigModule.forRoot
### `app.module.ts`
```bash
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ConfigModule } from '@nestjs/config';

@Module({
  imports: [ ConfigModule.forRoot({ isGlobal: true }) ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```
---


### Create service & controller
```bash
nest g service ev
```
```bash
nest g controller ev
```
##

### `ev.service.ts`
```bash
import { Injectable } from '@nestjs/common';
import { ConfigService } from '@nestjs/config'

@Injectable()
export class EvService {
    constructor(private configService: ConfigService) {}

    getDbUrl() {
        return this.configService.get<string>('DATABASE_URL');
    }
}
```
##


### `ev.controller.ts`
```bash
import { Controller, Get } from '@nestjs/common';
import { EvService } from './ev.service';

@Controller('ev')
export class EvController {
    constructor(private readonly evService: EvService) {}
    @Get()
    getUrl() {
        return this.evService.getDbUrl();
    }
}
```
##
><img width="379" height="116" alt="image" src="https://github.com/user-attachments/assets/383941e8-662e-4d1f-9894-3884f2133ce5" />

---

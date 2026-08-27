# Environment Variables

### install @nestjs/config
```bash
npm i @nestjs/config
```
---


> root e .env file toiri koro
### `.env`
```bash
# .env
DATABASE_URL=mongodb://localhost:500/mongodb
JWT_SECRET=1234567
```
---


>Module e import koro- ConfigModule.forRoot
### `app.module.ts`
```bash
import { MiddlewareConsumer, Module, NestModule } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UserController } from './user/user.controller';
import { ProductService } from './product/product.service';
import { ProductController } from './product/product.controller';
import { EmployeeModule } from './employee/employee.module';
import { CategoryModule } from './category/category.module';
import { StudentModule } from './student/student.module';
import { CustomerModule } from './customer/customer.module';
import { MynameController } from './myname/myname.controller';
import { UserRolesController } from './user-roles/user-roles.controller';
import { ExceptionController } from './exception/exception.controller';
import { LoggerMiddleware } from './middleware/logger/logger.middleware';
import { DatabaseService } from './database/database.service';
import { DatabaseController } from './database/database.controller';
import { ConfigModule } from '@nestjs/config';

@Module({
  imports: [EmployeeModule, CategoryModule, StudentModule, CustomerModule, ConfigModule.forRoot({
    isGlobal: true,
  })],
  controllers: [AppController, UserController, ProductController, MynameController, UserRolesController, ExceptionController, DatabaseController],
  providers: [AppService, ProductService, DatabaseService],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer){
    consumer.apply(LoggerMiddleware).forRoutes('*');
  } 
}
```
---


### Create service & controller
```bash
nest g service ev
```
```bash
nest g controller ev
```
---

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
---


##

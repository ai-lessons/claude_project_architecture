# Project Architecture Overview

**Проект:** ChatOpenAI Integration Assistant  
**Версия:** 1.3  
**Дата обновления:** 2025-01-31  
**Статус:** Активная разработка

---

## 📊 Technology Stack

### Frontend
- **Framework:** React 18 + TypeScript + Vite
- **State Management:** Zustand (useStore)
- **UI/CSS:** Tailwind CSS + Lucide React icons
- **Routing:** React Router (если используется)

### Backend & Infrastructure  
- **Database:** Supabase (PostgreSQL)
- **Authentication:** Supabase Auth
- **File Storage:** OpenAI Files API (НЕ Supabase Storage)
- **AI Integration:** OpenAI Assistants API + Embeddings API

### Key Dependencies
```json
{
  "@supabase/supabase-js": "^2.56.0",
  "openai": "^5.16.0", 
  "zustand": "state management",
  "react": "^18.3.1",
  "lucide-react": "^0.344.0"
}
```

---

## 🗂️ Project Structure

```
src/
├── components/           # React компоненты
│   ├── Personalities.tsx # Управление ассистентами + файлы
│   ├── FileDropZone.tsx  # Drag & drop компонент
│   ├── ChatArea.tsx      # Интерфейс чата
│   └── Sidebar.tsx       # Навигация
├── lib/                  # Сервисы и утилиты
│   ├── supabase.ts       # Supabase client + типы
│   ├── openai.ts         # OpenAI API service
│   ├── fileProcessing.ts # Обработка файлов
│   └── ragService.ts     # RAG сервис (legacy)
├── store/
│   └── useStore.ts       # Zustand store
└── App.tsx

supabase/
├── docs/                 # Документация БД
│   └── DATABASE_CHANGELOG.md
├── scripts/              # Миграции и скрипты
└── migrations/           # SQL миграции
```

---

## 🏗️ Core Architecture Decisions

### 1. Файловая архитектура: OpenAI Files API

**Решение:** Файлы хранятся в OpenAI, НЕ в нашей БД  
**Обоснование:**
- ✅ Нативная интеграция с Assistants API
- ✅ Автоматическая векторизация и поиск  
- ✅ Меньше сложности в инфраструктуре
- ✅ Воспроизведение логики Custom GPT

**Альтернативы рассмотрены:**
- ❌ Supabase Storage + собственная RAG система
- ❌ Локальное хранение + векторизация

**Структура данных:**
```typescript
// В БД храним только метаданные:
files: PersonalityFile[] = [
  {
    openai_file_id: "file-abc123", // ID в OpenAI
    file_name: "document.pdf",
    file_size: 1024000,
    status: "ready" | "processing" | "error"
  }
]
```

### 2. State Management: Zustand

**Решение:** Zustand вместо Redux/Context API  
**Обоснование:**
- ✅ Простота использования
- ✅ TypeScript поддержка  
- ✅ Минимальный boilerplate
- ✅ Отличная производительность

### 3. Database: JSONB vs Relational

**Решение:** JSONB для файлов, реляционная структура для основных данных  
**Обоснование:**
- ✅ `personalities.files` как JSONB массив - гибкость
- ✅ PostgreSQL отлично поддерживает JSONB
- ✅ Меньше JOIN'ов при чтении данных
- ✅ Atomic updates файлового массива

---

## 🔧 Key Services & Components

### OpenAI Service (src/lib/openai.ts)
**Назначение:** Взаимодействие с OpenAI API  
**Ключевые методы:**
```typescript
- createAssistant() → создание ассистента с транслитерацией имени
- updateAssistant() → обновление промпта + file_instruction  
- uploadFileToOpenAI() → загрузка файла в OpenAI Files API ✅
- deleteFileFromOpenAI() → удаление файла из OpenAI ✅
- listFiles() → список всех файлов ассистента ✅
- runAssistant() → запуск чата с оптимизированным polling
- checkRun() → проверка статуса без дублирования
```

**Архитектурные особенности:**
- Транслитерация кириллицы → латиница для OpenAI
- Системный промпт = base_prompt + file_instruction  
- Polling с минимальными API-вызовами

### Zustand Store (src/store/useStore.ts)
**Назначение:** Центральное состояние приложения  
**Структура:**
```typescript
AppState {
  // Auth
  user: User | null
  
  // Chats
  chats: Chat[]
  messages: Message[] 
  currentChatId: string | null
  
  // Personalities  
  personalities: Personality[]
  activePersonality: Personality | null
  
  // Services
  openaiService: OpenAIService
}
```

**Ключевые методы:**
- `sendMessage()` → отправка сообщения с оптимизированным polling
- `updatePersonality()` → обновление + синхронизация с OpenAI
- `uploadPersonalityFile()` → координация загрузки файлов ✅
- `deletePersonalityFile()` → удаление файла с обновлением ассистента ✅

### FileDropZone Component (src/components/FileDropZone.tsx) ✨ NEW
**Назначение:** Переиспользуемый drag & drop компонент  
**Особенности:**
- Полная drag & drop функциональность
- Визуальные индикаторы состояния (hover, active, error)
- Компактный режим для разных UI контекстов
- Встроенная валидация файлов
- TypeScript типизация props

### Database Layer (src/lib/supabase.ts)
**Назначение:** Типизированный доступ к Supabase  
**Особенности:**
- Строгие TypeScript типы для всех таблиц
- PersonalityFile интерфейс для JSONB структуры
- RLS (Row Level Security) политики

---

## 📡 Data Flow & Integration Patterns

### 1. Создание/обновление Personality
```
UI Form → useStore.updatePersonality() → 
├── Update Supabase DB
├── openaiService.updateAssistant() (системный промпт)  
└── UI State Update
```

### 2. Chat Message Flow
```
User Input → useStore.sendMessage() →
├── Add to local messages[]
├── Save to Supabase  
├── openaiService.addMessage() → OpenAI Thread
├── openaiService.runAssistant() → Start run
├── Optimized polling checkRun()  
├── Get response from Thread
└── Update UI + Save to DB
```

### 3. File Upload Flow (планируется)
```
File Selection → uploadPersonalityFile() →
├── openaiService.uploadFileToOpenAI() → file_id
├── Update personality.files[] в БД
├── openaiService.updateAssistant() → обновить промпт  
└── UI refresh
```

---

## 🎯 Development Standards

### Code Organization
- **1 компонент = 1 файл**
- **Сервисы в lib/** для переиспользования
- **TypeScript строгий** - no any (кроме исключений)
- **Именование:** camelCase для переменных, PascalCase для компонентов

### Database Patterns  
- **UUID** для всех Primary Keys
- **JSONB** для сложных структур данных
- **RLS** для безопасности на уровне строк
- **Миграции** через scripts с логированием

### Error Handling
- **Try/catch** в async функциях
- **User-friendly** сообщения об ошибках
- **Консольное логирование** для отладки
- **Fallback состояния** в UI

### Performance Optimizations  
- **Оптимизированный polling** OpenAI API
- **Zustand selective subscriptions**
- **GIN индексы** для JSONB queries
- **Минимальные re-renders** в React

---

## 📋 Current Implementation Status

### ✅ Готово (v1.2)
- [x] Базовый чат с ассистентами
- [x] Управление personalities  
- [x] OpenAI integration + polling optimization
- [x] Транслитерация имен для OpenAI
- [x] JSONB структура для файлов
- [x] Database cleanup от legacy полей

### ✅ Готово (v1.3)
- [x] File upload к ассистентам  
- [x] UI для управления файлами
- [x] Drag & drop интерфейс

### 🚧 В разработке
- [ ] Integration testing для file upload
- [ ] Error handling improvements

### 📋 Планируется  
- [ ] Function calling для ассистентов
- [ ] Advanced file types support
- [ ] Export/import чатов
- [ ] Аналитика использования

---

## 🔄 Evolution & Migration Strategy

### Подход к изменениям
1. **Документировать решение** в этом файле
2. **Database changes** → DATABASE_CHANGELOG.md
3. **Backward compatibility** когда возможно
4. **Feature flags** для экспериментальной функциональности

### Migration Pattern
```
Planning → Implementation → Testing → Documentation → Deployment
    ↓           ↓              ↓           ↓            ↓
  This file  Code+Tests    Manual QA   Update docs   Git push
```

---

*Документ поддерживается в актуальном состоянии для эффективной разработки*  
*Последнее обновление: 2025-01-31*
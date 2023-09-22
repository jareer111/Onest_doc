# Onest Filter Documentation

Bu dokumentatsiya Onest filtrlarini ishlatish haqida ma'lumotlar taqdim etadi.

### Filter tavsifi

- **"filter_key"**: Bu filter qilmoqchi bulgan fildizni nomi.
- **"value"**: Bu filter qilmoqchi bulgan fildizni qiymati.
- **"operator"**: Bu filter qilmoqchi bulgan fildizni operatori (bu operatorlar: "cn", "eq", "gte", "lte").
  - "cn" -> CONTAINS
  - "eq" -> EQUAL
  - "gte" -> GREATER THAN OR EQUAL
  - "lte" -> LESS THAN OR EQUAL
- **"data_option"**: Bu **"all"** yoki **"any"** bo'lishi mumkin. **"all"** tanlangan bo'lsa, shakillantirilgan filterning hamma **Ad(Reklama)** da bo'lishi kerak.
    Agar **"any"** tanlangan bo'lsa, shakillantirilgan filterdan biri **Ad** da bo'lishi kerak.

   **_Eslatma:_** Agar filterda bitta **"filter_key"** bir nechta marta qatnashsa, **"all"** ni ishlating; agar bir necha marta ishlatilsa, **"any"** ni ishlating, chunki **"any"** siz berilgan bir **"filter_key"** ichidagi bir nechta qiymatlarni qo'llab-quvvatlaydi.

### Filterlar

1. **"cn" -> CONTAINS** operatori orqali **["title"]** bo'yicha filter qilish:

   **Example:**
```json
{
  "filters": [
    {
      "filter_key": "title",
      "value": "chilonzor 12",
      "operator": "cn",
      "data_option": "all"
    }
  ]
}
```

**2. "eq" -> EQUAL** operatori orqali **["amenity", "districtName", "regionName", "price", "area", "countOfRooms", "floor", "countOfFloors"]** bo'yicha filter qilish mumkin:

2.1 Amenities (udobstva) uchun:

   **Example:**
```json
{
  "filters": [
    {
      "filter_key": "amenity",
      "value": "lux",
      "operator": "eq",
      "data_option": "any"
    },
    {
      "filter_key": "amenity",
      "value": "parking",
      "operator": "eq",
      "data_option": "any"
    }
   ]
 }
```
  2.2 Agar siz **districtName** (Ташкентский район) ni filter qilmoqchi bulsayiz unda  siz shu kurinishda filterni shakllantirishingiz kerak.
   **"value"** ga District dagi **'search_name'** fildini kiritasiz **ex:** 'yakkasaroy' yoki 'yashnobod'...

   **Example:**
```json
   {
     "filters": [
        {
         "filter_key": "districtName",
         "value": "yunusobod",
         "operator": "eq",
         "data_option": "all"
        }
      ]
   }

```

  2.3 Agar siz **regionName** (Ташкент) ni filter qilmoqchi bulsayiz unda  siz shu kurinishda filterni shakllantirishingiz kerak.
   **"value"** ga Region dagi **'search_name'** fildini kiritasiz **ex:** 'tashkent' yoki 'fergana'...

   **Example:**
```json
   {
    "filters": [
       {
        "filter_key": "regionName",
        "value": "tashkent",
        "operator": "eq",
        "data_option": "all"
       }
     ]
   }
   ```

 2.4 Agar siz **'countOfRooms'** (xona soni) ni **'n'** ga teng busin desangiz. **"countOfRooms"** ni urniga **["price", "area", "countOfRooms", "floor", "countOfFloors"]** ishlatishingiz mumkin.
     Eslatma agar siz bitta filterda bir bitta fildni bir necha marta ishlatmoqchi bulsangiz unda **"data_option"** ni **"any"** qilib qo'yishingiz kerak.

   **Example:**
```json
   {
    "filters": [
       {
        "filter_key": "countOfRooms",
        "value": "2",
        "operator": "eq",
        "data_option": "any"
       },{
        "filter_key": "countOfRooms",
        "value": "3",
        "operator": "eq",
        "data_option": "any"
        }
     ]
   }
   ```

**3. "gte"** & **"lte"** => Bu operator orqali siz **["price", "area", "countOfRooms", "floor", "countOfFloors"]** buyicha filter qilishingiz mumkin.

 3.1 Agar siz **"price"** (narx) ni filter qilmoqchi bulsayiz unda  siz shu kurinishda filterni shakllantirishingiz kerak.
     **"price"** ni urniga  **["price", "area", "countOfRooms", "floor", "countOfFloors"]** ga ham shu kurinishda filter shakillantirishingiz mumkin.

   **Example:**
```json
   {
    "filters": [
       {
        "filter_key": "price",
        "value": "min",
        "operator": "gte",
        "data_option": "any"
       },{
        "filter_key": "price",
        "value": "max",
        "operator": "lte",
        "data_option": "any"
       }
     ]
   }
   ```

**4.** Siz bir vaxtning uzida bir nechta fiterlarni shakillantirishingiz mumkin.

   **Example:**
   
   ```json
        {
         "filters": [
            {
             "filter_key": "title",
             "value": "Reklama nomi misol uchun",
             "operator": "cn",
             "data_option": "all"
            },{
             "filter_key": "amenity",
             "value": "lux",
             "operator": "eq",
             "data_option": "all"
            },{
             "filter_key": "regionName",
             "value": "tashkent"
             "operator": "eq",
             "data_option": "all"
            },{
             "filter_key": "price",
             "value": "min",
             "operator": "gte",
             "data_option": "any"
            },{
             "filter_key": "price",
             "value": "max",
             "operator": "lte",
             "data_option": "any"
            },{
             "filter_key": "countOfRooms",
             "value": "min",
             "operator": "gte",
             "data_option": "any"
            },{
             "filter_key": "countOfRooms",
             "value": "max",
             "operator": "lte",
             "data_option": "any"
            }
          ]
        }
```

_Eslatma!:_ Agar siz shu operatorlarning urniga  boshqa operator ishlatsayiz  [**"Unsupported filter operation!"** ] degan hatolik olasiz.

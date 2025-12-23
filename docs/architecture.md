# Mimari Özeti

Katmanlı yapı:
- `features/*/domain`: entity ve repository kontratları
- `features/*/data`: Firestore/Storage implementasyonları
- `features/*/presentation`: BLoC ve UI (pages/widgets)
- `services/messaging_service.dart`: FCM abonelik, foreground/klik navigasyonu
- `lib/main.dart`: provider’lar, tema, auth wrapper

Veri akışı (rapor):
1) `CreateReportPage` formu → `ReportBloc` → `ReportRepositoryFirestore.createReport()`
2) Firestore `reports` akışı → `ReportBloc.streamReports()` → Home list + harita pinleri
3) Detay ekranında admin durum/açıklama değişimi → repo `updateStatus()`/`updateReportDescription()`
4) Takip toggle → `report_follows` koleksiyonu
5) Acil uyarı: Detay ekranından `alerts` dokümanı eklenir; 2. günde Cloud Functions ile `alerts` topic’e FCM push atılacak.

Koleksiyonlar:
- `users`, `reports`, `report_follows`, `alerts`

Roller:
- `user`, `admin` (users/{uid}.role)

Harita:
- `flutter_map` + OSM, tür bazlı renk/ikon, pin kartı ve detay geçişi.

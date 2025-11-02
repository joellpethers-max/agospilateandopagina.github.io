rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Usuarios pueden leer/escribir sus propios datos
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      
      // Subcolecciones
      match /purchases/{purchaseId} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
      
      match /pendingPayments/{paymentId} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
      
      match /progress/{courseId} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
}

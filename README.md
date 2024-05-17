# Appreciate-App-Project

@startuml
entity user {
  user_id : int auto_increment not_null <PK>
  email : text not_null
  password : text not_null
  username : text not_null 
  --
  profile_picture : image 
  bio : text 
  followers : int default 0
  following : int default 0
}

entity user_private_chat {
  chat_id : int not_null auto_increment <PK>
  sender_id : int not null <FK>
  receiver_id : int not null <FK>
  --
  content : text/image not_null
  create_at : date_time not_null
}

entity post {
  post_id : int auto_increment not_null <PK>
  user_id : int not_null <FK>
  --
  content : text/image/mp4 not_null 
  uppvote : int default 0
  downvote : int default 0
  created_at : date_time not_null
}

entity comment {
  comment_id : int not_null auto_increment <PK>
  post_id : int not_null <FK>
  user_id : int not_null <FK>
  --
  content : text not_null
  created_at : date_time not_null
}

entity community {
  community_id : int not_null auto_increment <PK>
  community_name : text not_null 
  --
  description_id : text 
  community_picture : image
  created_at : date_time not_null

}

entity community_chat {
   message_id : int not_null auto_increment <PK>
   community_id : int not_null <FK>
   user_id : int not_null <FK>
   --
   content : text/image not_null
   sent_at : date_time not_null
}

entity membership_community {
  member_id : int not_null auto_increment <PK>
  community_id : int not_null <FK>
  user_id : int not_null <FK>
  -- 
  role : text not_null enum
  joined_at : date_time not_null
}

entity notification{
  notification_id : int not_null auto_increment <PK>
  user_id : int not_null <FK>
  --
  type : text enum not_null
  is_read : boolean
  created_at : date_time not_null
  
}

user ||-- user_private_chat
user_private_chat --o{ user

user ||--o{ post
note on link
Membuat
end note

user --> community
note on link
CRUD
end note

user }o-- membership_community
membership_community --o{ community

user ||-- community_chat
community_chat --o{ community

comment --|| user
comment --o{ post

user ||-- notification
user ||-- notification

user --> post
note on link
up/down vote, CRUD
end note

user --> user
note on link
report
end note

user --> post
note on link
report
end note

user --> post
note on link
save
end note

user --> community
note on link
report 
end note
@enduml

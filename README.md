#

rails new friendship-model-2
rails g model User name
rails g model Friendship user:references friend_id:integer confirmed:boolean

add=>
, default: false
add_foreign_key :friends, :user, column: :friend_id

seed=>
names = ["Kubilay","Tayo","Berry", "Dennis"]

names.each do |name|
  User.create(name: name)
end

Friend.create(user_id: 2, friend_id: 1)
Friend.create(user_id: 2, friend_id: 3, confirmed: true)
Friend.create(user_id: 2, friend_id: 4, confirmed: true)

Friend.create(user_id: 1, friend_id: 2, confirmed: true)
Friend.create(user_id: 1, friend_id: 3)
Friend.create(user_id: 1, friend_id: 4, confirmed: true)

models=>

#

rails new friendship-model-2
rails g model User name
rails g model Friendship user:references friend_id:integer confirmed:boolean

add=>
, default: false
add_foreign_key :friendships, :users, column: :friend_id

seed=>
names = ["Kubilay","Tayo","Berry", "Dennis"]

names.each do |name|
  User.create(name: name)
end

Friendship.create(user_id: 2, friend_id: 1)
Friendship.create(user_id: 2, friend_id: 3, confirmed: true)
Friendship.create(user_id: 2, friend_id: 4, confirmed: true)

Friendship.create(user_id: 1, friend_id: 2, confirmed: true)
Friendship.create(user_id: 1, friend_id: 3)
Friendship.create(user_id: 1, friend_id: 4, confirmed: true)

models=>
class User < ApplicationRecord
  has_many :confirmed_friendships, -> { confirmed }, class_name: 'Friendship'
  has_many :friends, source: :friend, through: :confirmed_friendships
end

class Friendship < ApplicationRecord
  belongs_to :friend, class_name: 'User', foreign_key: 'friend_id'

  scope :confirmed, -> { where(confirmed: true) }
end

rails db:migrate
rails db:seed

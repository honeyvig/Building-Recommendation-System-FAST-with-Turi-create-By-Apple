# Building-Recommendation-System-FAST-with-Turi-create-By-Apple
To build a recommendation system quickly with Turi Create (which is a framework by Apple), you can follow these steps. Turi Create is a machine learning library designed to simplify the development of recommendation systems, among other tasks. It's easy to use and works well with structured data, making it a great option for beginners.

Here’s how you can quickly create a recommendation system using Turi Create:
Step 1: Install Turi Create

First, you'll need to install Turi Create. You can do this via pip:

pip install turicreate

Step 2: Prepare Your Data

For a recommendation system, you usually need a dataset that includes user-item interactions, such as ratings, views, or purchases. Here's an example of how your data might look in a CSV file:

user_id, item_id, rating
1, 101, 5
2, 102, 3
1, 103, 4
3, 101, 2
...

Step 3: Load and Prepare Data

Now, let’s load the data and prepare it for Turi Create.

import turicreate as tc

# Load data (you can replace 'data.csv' with the actual path to your dataset)
data = tc.SFrame('data.csv')

# Inspect the first few rows to confirm
print(data.head())

Step 4: Build the Recommendation Model

Turi Create provides an easy way to build a recommendation model using turicreate.recommender.create.

# Build a recommendation model based on user-item interactions
model = tc.recommender.create(data, user_id='user_id', item_id='item_id', target='rating')

# Print out a summary of the model
model.summary()

In the above code:

    user_id: The column in your data that identifies users.
    item_id: The column that identifies the items (e.g., movies, products, etc.).
    target: The column that represents ratings, views, or interactions.

Step 5: Make Recommendations

Once the model is trained, you can use it to make recommendations for users. Here's how you can recommend items to a specific user:

# Recommend 5 items for user with user_id = 1
recommendations = model.recommend(users=[1], num_items=5)

# Show the recommendations
recommendations.print_rows(num_rows=5)

This will give you the top 5 items recommended for user 1.
Step 6: Evaluate the Model

To evaluate how well your model performs, you can use a test dataset. Here's an example of how to split the data and evaluate the model:

# Split data into training and testing sets
train_data, test_data = data.random_split(0.8)

# Create the model with training data
model = tc.recommender.create(train_data, user_id='user_id', item_id='item_id', target='rating')

# Evaluate the model on the test data
evaluation = model.evaluate(test_data)
print(evaluation)

Step 7: Save the Model

If you're satisfied with the model, you can save it for future use:

# Save the model
model.save('recommender_model')

Step 8: Load the Model and Make Predictions Later

If you saved the model, you can reload it and make recommendations at a later time:

# Load the saved model
model = tc.load_model('recommender_model')

# Get recommendations for user 1 again
recommendations = model.recommend(users=[1], num_items=5)
recommendations.print_rows(num_rows=5)

That's it! You've quickly built a recommendation system using Turi Create. The beauty of Turi Create lies in its simplicity and speed, letting you prototype and experiment with recommendation systems efficiently.

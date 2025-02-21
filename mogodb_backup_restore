from pymongo import MongoClient

def transfer_all_files(source_conn_str, source_db_name, target_conn_str, target_db_name):
    # Connect to source MongoDB
    source_client = MongoClient(source_conn_str)
    source_db = source_client[source_db_name]

    # Connect to target MongoDB
    target_client = MongoClient(target_conn_str)
    target_db = target_client[target_db_name]

    # Get all collections in the source database
    collections = source_db.list_collection_names()

    for collection_name in collections:
        source_collection = source_db[collection_name]
        target_collection = target_db[collection_name]

        # Transfer all documents from source to target collection
        documents = source_collection.find()
        if source_collection.count_documents({}) > 0:
            target_collection.insert_many(documents)

    # Close the connections
    source_client.close()
    target_client.close()

# Example usage
source_conn_str = "mongodb://source_host:source_port"
source_db_name = "source_database"
target_conn_str = "mongodb://target_host:target_port"
target_db_name = "target_database"

transfer_all_files(source_conn_str, source_db_name, target_conn_str, target_db_name)

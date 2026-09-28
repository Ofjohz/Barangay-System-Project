TITLE = "BARANGAY CLEARANCE SYSTEM"

users = {
    "residents": {},
    "admins": {
        "Administrator": {
            "password": "admin123",
            "name": "Barangay Administrator"
        }
    },
    "staff": {
        "StaffAssistant": {
            "password": "staff123",
            "name": "Barangay Staff"
        }
    }
}

requests = []
payments = []
clearances = []

resident_id = 1
request_id = 1001
payment_id = 1


def create_account():
    global resident_id

    print("\nCREATE RESIDENT ACCOUNT")

    username = input("Username: ").strip()

    if username in users["residents"]:
        print("Username already exists.")
        return

    password = input("Password: ").strip()
    confirm_password = input("Confirm Password: ").strip()

    if password != confirm_password:
        print("Passwords do not match.")
        return

    full_name = input("Full Name: ").strip()
    address = input("Address: ").strip()
    contact_number = input("Contact Number: ").strip()
    birth_date = input("Date of Birth: ").strip()
    valid_id = input("Valid ID/Reference Number: ").strip()

    users["residents"][username] = {
        "resident_id": resident_id,
        "username": username,
        "password": password,
        "full_name": full_name,
        "address": address,
        "contact_number": contact_number,
        "birth_date": birth_date,
        "valid_id": valid_id
    }

    print("\nAccount created successfully.")
    print("Resident ID:", resident_id)

    resident_id += 1


def resident_login():
    print("\nRESIDENT LOGIN")

    username = input("Username: ").strip()
    password = input("Password: ").strip()

    if username not in users["residents"]:
        print("Account not found.")
        return

    if users["residents"][username]["password"] != password:
        print("Incorrect password.")

        print("\n1. Try Again")
        print("2. Forgot Password")
        print("3. Back")

        choice = input("Enter choice: ")

        if choice == "2":
            forgot_password()

        return

    print("\nLogin successful.")
    resident_menu(username)


def admin_login():
    print("\nADMIN LOGIN")

    username = input("Username: ").strip()
    password = input("Password: ").strip()

    if username not in users["admins"]:
        print("Admin account not found.")
        return

    if users["admins"][username]["password"] != password:
        print("Incorrect password.")
        return

    print("\nLogin successful.")
    admin_menu(username)


def staff_login():
    print("\nSTAFF LOGIN")

    username = input("Username: ").strip()
    password = input("Password: ").strip()

    if username not in users["staff"]:
        print("Staff account not found.")
        return

    if users["staff"][username]["password"] != password:
        print("Incorrect password.")
        return

    print("\nLogin successful.")
    staff_menu(username)


def forgot_password():
    print("\nFORGOT PASSWORD")

    username = input("Username: ").strip()

    if username not in users["residents"]:
        print("Account not found.")
        return

    contact_number = input("Registered Contact Number: ").strip()

    if contact_number != users["residents"][username]["contact_number"]:
        print("Contact number does not match.")
        return

    new_password = input("New Password: ").strip()
    confirm_password = input("Confirm New Password: ").strip()

    if new_password != confirm_password:
        print("Passwords do not match.")
        return

    users["residents"][username]["password"] = new_password

    print("Password changed successfully.")


def resident_menu(username):
    while True:
        print("\nRESIDENT MENU")
        print("1. View Profile")
        print("2. Request Barangay Clearance")
        print("3. Check Request Status")
        print("4. View Previous Requests")
        print("5. Change Password")
        print("6. Logout")

        choice = input("Enter choice: ")

        if choice == "1":
            view_profile(username)

        elif choice == "2":
            request_clearance(username)

        elif choice == "3":
            check_request_status(username)

        elif choice == "4":
            view_previous_requests(username)

        elif choice == "5":
            change_resident_password(username)

        elif choice == "6":
            print("Logged out.")
            break

        else:
            print("Invalid choice.")


def view_profile(username):
    resident = users["residents"][username]

    print("\nRESIDENT PROFILE")
    print("Resident ID:", resident["resident_id"])
    print("Username:", resident["username"])
    print("Full Name:", resident["full_name"])
    print("Address:", resident["address"])
    print("Contact Number:", resident["contact_number"])
    print("Date of Birth:", resident["birth_date"])
    print("Valid ID:", resident["valid_id"])


def request_clearance(username):
    global request_id

    print("\nREQUEST BARANGAY CLEARANCE")

    purpose = input("Purpose of Clearance: ").strip()
    date_requested = input("Date Requested: ").strip()

    if purpose == "":
        print("Purpose cannot be empty.")
        return

    new_request = {
        "request_id": request_id,
        "resident_id": users["residents"][username]["resident_id"],
        "username": username,
        "full_name": users["residents"][username]["full_name"],
        "purpose": purpose,
        "date_requested": date_requested,
        "status": "Pending"
    }

    requests.append(new_request)

    print("\nClearance request submitted.")
    print("Request Number:", request_id)
    print("Status: Pending")

    request_id += 1


def check_request_status(username):
    print("\nREQUEST STATUS")

    found = False

    for request in requests:
        if request["username"] == username:
            found = True

            print("\nRequest Number:", request["request_id"])
            print("Purpose:", request["purpose"])
            print("Date Requested:", request["date_requested"])
            print("Status:", request["status"])

            for payment in payments:
                if payment["request_id"] == request["request_id"]:
                    print("Clearance Fee:", payment["amount"])
                    print("Payment Status:", payment["payment_status"])
                    print("Date Paid:", payment["date_paid"])

    if found == False:
        print("No clearance request found.")


def view_previous_requests(username):
    print("\nPREVIOUS CLEARANCE REQUESTS")

    found = False

    for request in requests:
        if request["username"] == username:
            found = True

            print("\nRequest Number:", request["request_id"])
            print("Purpose:", request["purpose"])
            print("Date Requested:", request["date_requested"])
            print("Status:", request["status"])

    if found == False:
        print("No previous requests found.")


def change_resident_password(username):
    print("\nCHANGE PASSWORD")

    old_password = input("Current Password: ")

    if old_password != users["residents"][username]["password"]:
        print("Incorrect current password.")
        return

    new_password = input("New Password: ")
    confirm_password = input("Confirm New Password: ")

    if new_password != confirm_password:
        print("Passwords do not match.")
        return

    users["residents"][username]["password"] = new_password

    print("Password changed successfully.")


def admin_menu(username):
    while True:
        print("\nADMIN MENU")
        print("1. View Requests")
        print("2. Search Resident")
        print("3. Approve Request")
        print("4. Reject Request")
        print("5. Update Request Status")
        print("6. View Payment Records")
        print("7. Clearance Menu")
        print("8. Change Password")
        print("9. Logout")

        choice = input("Enter choice: ")

        if choice == "1":
            view_all_requests()

        elif choice == "2":
            search_resident()

        elif choice == "3":
            approve_request()

        elif choice == "4":
            reject_request()

        elif choice == "5":
            update_request_status()

        elif choice == "6":
            view_payments()

        elif choice == "7":
            clearance_menu()

        elif choice == "8":
            change_admin_password(username)

        elif choice == "9":
            print("Logged out.")
            break

        else:
            print("Invalid choice.")


def staff_menu(username):
    while True:
        print("\nSTAFF MENU")
        print("1. View Requests")
        print("2. Search Resident")
        print("3. Approve Request")
        print("4. Reject Request")
        print("5. Update Request Status")
        print("6. View Payment Records")
        print("7. Clearance Menu")
        print("8. Change Password")
        print("9. Logout")

        choice = input("Enter choice: ")

        if choice == "1":
            view_all_requests()

        elif choice == "2":
            search_resident()

        elif choice == "3":
            approve_request()

        elif choice == "4":
            reject_request()

        elif choice == "5":
            update_request_status()

        elif choice == "6":
            view_payments()

        elif choice == "7":
            clearance_menu()

        elif choice == "8":
            change_staff_password(username)

        elif choice == "9":
            print("Logged out.")
            break

        else:
            print("Invalid choice.")


def view_all_requests():
    print("\nALL CLEARANCE REQUESTS")

    if len(requests) == 0:
        print("No requests found.")
        return

    for request in requests:
        print("\nRequest Number:", request["request_id"])
        print("Resident:", request["full_name"])
        print("Purpose:", request["purpose"])
        print("Date Requested:", request["date_requested"])
        print("Status:", request["status"])


def search_resident():
    print("\nSEARCH RESIDENT")

    search = input("Enter resident name or request number: ").strip()

    found = False

    for resident in users["residents"].values():
        if search.lower() in resident["full_name"].lower():
            found = True

            print("\nResident ID:", resident["resident_id"])
            print("Full Name:", resident["full_name"])
            print("Address:", resident["address"])
            print("Contact Number:", resident["contact_number"])
            print("Date of Birth:", resident["birth_date"])
            print("Valid ID:", resident["valid_id"])

    for request in requests:
        if search == str(request["request_id"]):
            found = True

            print("\nREQUEST FOUND")
            print("Request Number:", request["request_id"])
            print("Resident:", request["full_name"])
            print("Purpose:", request["purpose"])
            print("Date Requested:", request["date_requested"])
            print("Status:", request["status"])

    if found == False:
        print("No record found.")


def approve_request():
    print("\nAPPROVE REQUEST")

    try:
        number = int(input("Enter Request Number: "))
    except:
        print("Invalid request number.")
        return

    for request in requests:
        if request["request_id"] == number:

            if request["status"] != "Pending":
                print("This request is already", request["status"])
                return

            request["status"] = "Approved"

            print("Request approved.")
            print("Request Number:", request["request_id"])

            add_payment(request)

            return

    print("Request not found.")


def reject_request():
    print("\nREJECT REQUEST")

    try:
        number = int(input("Enter Request Number: "))
    except:
        print("Invalid request number.")
        return

    for request in requests:
        if request["request_id"] == number:

            if request["status"] != "Pending":
                print("This request is already", request["status"])
                return

            request["status"] = "Rejected"

            print("Request rejected.")
            print("Request Number:", request["request_id"])

            return

    print("Request not found.")


def update_request_status():
    print("\nUPDATE REQUEST STATUS")
    print("1. Approved")
    print("2. Rejected")
    print("3. Released")

    choice = input("Enter choice: ")

    try:
        number = int(input("Enter Request Number: "))
    except:
        print("Invalid request number.")
        return

    for request in requests:
        if request["request_id"] == number:

            if choice == "1":
                if request["status"] == "Rejected":
                    print("Rejected request cannot be approved.")
                    return

                request["status"] = "Approved"

                print("Request status updated.")
                print("Request Number:", request["request_id"])
                print("Status:", request["status"])

                return

            elif choice == "2":
                if request["status"] == "Released":
                    print("Released request cannot be rejected.")
                    return

                request["status"] = "Rejected"

                print("Request status updated.")
                print("Request Number:", request["request_id"])
                print("Status:", request["status"])

                return

            elif choice == "3":

                if request["status"] != "Approved":
                    print("Request must be Approved first.")
                    print("Current Status:", request["status"])
                    return

                payment_found = False
                payment_paid = False

                for payment in payments:
                    if payment["request_id"] == number:
                        payment_found = True

                        if payment["payment_status"].strip().lower() == "paid":
                            payment_paid = True

                if payment_found == False:
                    print("No payment record found.")
                    return

                if payment_paid == False:
                    print("Payment is not completed.")
                    print("Payment Status must be Paid.")
                    return

                request["status"] = "Released"

                print("\nRequest released successfully.")
                print("Request Number:", request["request_id"])
                print("Status:", request["status"])

                return

            else:
                print("Invalid choice.")
                return

    print("Request not found.")


def add_payment(request):
    global payment_id

    for payment in payments:
        if payment["request_id"] == request["request_id"]:
            return

    print("\nPAYMENT RECORD")

    amount = input("Clearance Fee: ")
    payment_status = input("Payment Status: ")
    date_paid = input("Date Paid: ")

    payment = {
        "payment_id": payment_id,
        "request_id": request["request_id"],
        "amount": amount,
        "payment_status": payment_status,
        "date_paid": date_paid
    }

    payments.append(payment)

    print("Payment record added.")

    payment_id += 1


def view_payments():
    print("\nPAYMENT RECORDS")

    if len(payments) == 0:
        print("No payment records found.")
        return

    for payment in payments:
        print("\nPayment ID:", payment["payment_id"])
        print("Request Number:", payment["request_id"])
        print("Clearance Fee:", payment["amount"])
        print("Payment Status:", payment["payment_status"])
        print("Date Paid:", payment["date_paid"])


def clearance_menu():
    while True:
        print("\nCLEARANCE MENU")
        print("1. Generate Barangay Clearance")
        print("2. View Generated Clearances")
        print("3. Back")

        choice = input("Enter choice: ")

        if choice == "1":
            generate_clearance()

        elif choice == "2":
            view_clearances()

        elif choice == "3":
            break

        else:
            print("Invalid choice.")


def generate_clearance():
    print("\nGENERATE BARANGAY CLEARANCE")

    try:
        number = int(input("Enter Request Number: "))
    except:
        print("Invalid request number.")
        return

    for request in requests:

        if request["request_id"] == number:

            print("Current Request Status:", request["status"])

            if request["status"].strip().lower() != "released":
                print("Clearance cannot be generated.")
                print("Request must have Released status.")
                return

            resident = users["residents"][request["username"]]

            for clearance in clearances:
                if clearance["request_id"] == number:
                    print("Clearance has already been generated.")
                    return

            barangay = input("Barangay Name: ")
            municipality = input("Municipality: ")
            province = input("Province: ")
            captain = input("Barangay Captain Name: ")
            issue_date = input("Date Issued: ")

            clearance = {
                "request_id": request["request_id"],
                "resident_id": resident["resident_id"],
                "full_name": resident["full_name"],
                "address": resident["address"],
                "birth_date": resident["birth_date"],
                "contact_number": resident["contact_number"],
                "valid_id": resident["valid_id"],
                "purpose": request["purpose"],
                "date_issued": issue_date,
                "barangay": barangay,
                "municipality": municipality,
                "province": province,
                "captain": captain
            }

            clearances.append(clearance)

            print("\nBarangay Clearance Generated Successfully.")

            print_clearance(clearance)

            return

    print("Request not found.")


def print_clearance(clearance):
    print("\n")
    print("REPUBLIC OF THE PHILIPPINES")
    print("PROVINCE OF", clearance["province"])
    print("MUNICIPALITY OF", clearance["municipality"])
    print("BARANGAY", clearance["barangay"])
    print("OFFICE OF THE BARANGAY CAPTAIN")

    print("\nBARANGAY CLEARANCE")

    print("\nThis is to certify that")
    print(clearance["full_name"])
    print("is a resident of Barangay", clearance["barangay"] + ",")
    print("and is known to be of good moral character")
    print("and a law-abiding citizen.")

    print("\nIt is further certified that the above-named person")
    print("has no derogatory or criminal record filed")
    print("in this barangay, based on the records available.")

    print("\nIssued this", clearance["date_issued"])
    print("upon request of the interested party")
    print("for whatever legal purpose this clearance may serve.")

    print("\nPurpose:", clearance["purpose"])
    print("Request Number:", clearance["request_id"])

    print("\n")
    print(clearance["captain"])
    print("Barangay Captain")

    print("\nCLEARANCE STATUS: RELEASED")


def view_clearances():
    print("\nGENERATED CLEARANCES")

    if len(clearances) == 0:
        print("No generated clearances found.")
        return

    for clearance in clearances:
        print("\nRequest Number:", clearance["request_id"])
        print("Resident:", clearance["full_name"])
        print("Barangay:", clearance["barangay"])
        print("Municipality:", clearance["municipality"])
        print("Province:", clearance["province"])
        print("Purpose:", clearance["purpose"])
        print("Date Issued:", clearance["date_issued"])
        print("Barangay Captain:", clearance["captain"])


def change_admin_password(username):
    print("\nCHANGE ADMIN PASSWORD")

    old_password = input("Current Password: ")

    if old_password != users["admins"][username]["password"]:
        print("Incorrect current password.")
        return

    new_password = input("New Password: ")
    confirm_password = input("Confirm New Password: ")

    if new_password != confirm_password:
        print("Passwords do not match.")
        return

    users["admins"][username]["password"] = new_password

    print("Admin password changed successfully.")


def change_staff_password(username):
    print("\nCHANGE STAFF PASSWORD")

    old_password = input("Current Password: ")

    if old_password != users["staff"][username]["password"]:
        print("Incorrect current password.")
        return

    new_password = input("New Password: ")
    confirm_password = input("Confirm New Password: ")

    if new_password != confirm_password:
        print("Passwords do not match.")
        return

    users["staff"][username]["password"] = new_password

    print("Staff password changed successfully.")


def main():
    while True:
        print("\n" + TITLE)
        print("1. Register Resident")
        print("2. Resident Login")
        print("3. Admin Login")
        print("4. Staff Login")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            create_account()

        elif choice == "2":
            resident_login()

        elif choice == "3":
            admin_login()

        elif choice == "4":
            staff_login()

        elif choice == "5":
            print("Thank you for using the Barangay Clearance System.")
            break

        else:
            print("Invalid choice.")


main()
